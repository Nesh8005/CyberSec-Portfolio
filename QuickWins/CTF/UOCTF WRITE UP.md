# ML Connoisseur - CTF Write-up

**Challenge:** ML Connoisseur  
**Category:** Machine Learning / Reverse Engineering  
**Difficulty:** Hard  
**Flag:** `uoftctf{m0d3l_1nv3R510N}`

## Table of Contents

1. [Initial Analysis](#initial-analysis)
2. [Understanding the Challenge](#understanding-the-challenge)
3. [Failed Attempt #1: Gradient Ascent](#failed-attempt-1-gradient-ascent)
4. [Failed Attempt #2: Weight Inspection](#failed-attempt-2-weight-inspection)
5. [Failed Attempt #3: ImageNet Hypothesis](#failed-attempt-3-imagenet-hypothesis)
6. [Failed Attempt #4: More ImageNet Classes](#failed-attempt-4-more-imagenet-classes)
7. [Failed Attempt #5: ML Culture Images](#failed-attempt-5-ml-culture-images)
8. [Failed Attempt #6: EMNIST Hypothesis](#failed-attempt-6-emnist-hypothesis)
9. [Breakthrough: Model Structure Analysis](#breakthrough-model-structure-analysis)
10. [The Solution: Model Inversion](#the-solution-model-inversion)
11. [Lessons Learned](#lessons-learned)

---

## Initial Analysis

When I first extracted the challenge files, I found:

- `chal.py` - The main challenge script  
- `model.py` - A PyTorch model definition (heavily obfuscated)
- `weights.pt` - Pre-trained model weights (104MB)
- `requirements.txt` - Dependencies
- `examples/` - Example images (0.png through 9.png)

The first thing I noticed was that `chal.py` looked weird - full of XOR operations and obfuscated strings. I asked ChatGPT for help understanding XOR deobfuscation patterns, and it suggested the strings were likely XOR-encoded with a single-byte key.

### Deobfuscating chal.py

I wrote a simple deobfuscation script to try different XOR keys:

```python
def xor_decrypt(data, key):
    return ''.join(chr(ord(c) ^ key) for c in data)

# Found in the file
obfuscated = "..."
for key in range(256):
    try:
        result = xor_decrypt(obfuscated, key)
        if 'import' in result or 'def' in result:
            print(f"Key {key}: {result}")
    except:
        pass
```

After testing, I found the key was **42**. The deobfuscated code revealed:

```python
import torch
from PIL import Image
import numpy as np
import model as model_obf

# Load and preprocess image
img = Image.open(sys.argv[1]).convert('RGB')
img = img.resize((256, 256), Image.BILINEAR)
arr = np.array(img, dtype=np.float32) / 255.0
tensor = torch.from_numpy(arr).permute(2, 0, 1).unsqueeze(0)

# Load model
for obj in model_obf.__dict__.values():
    if hasattr(obj, '__entry__') and obj.__entry__ is True:
        model_class = obj
        
model = model_class()
model.load_state_dict(torch.load("weights.pt"))
model.eval()

# Run inference
output = model(tensor)

# THE KEY PART:
if int(output.item()) > 9:
    print("you got it!")
else:
    print(int(output.item()))
```

**The trigger condition:** If the model outputs a value > 9 (and we cast to int), we get the flag!

---

## Understanding the Challenge

I tested the provided examples first:

```bash
python chal.py examples/0.png  # Output: 0
python chal.py examples/1.png  # Output: 1
python chal.py examples/5.png  # Output: 5
python chal.py examples/9.png  # Output: 9
```

So it's a digit classifier that works correctly on 0-9. But we need an output **> 9**, which means either:

1. There's a hidden class 10+ in the model
2. The model has a special backdoor/easter egg
3. We need to craft an adversarial input

---

## Failed Attempt #1: Gradient Ascent

My first idea was to use **activation maximization** - generate an image that maximizes the model's output. I thought if I could push the output value high enough, it might exceed 9.

I wrote this script (with some help from ChatGPT on the PyTorch autograd syntax):

```python
import torch
import torch.nn.functional as F
from PIL import Image
import numpy as np
import model as model_obf

# Load model
model_class = None
for obj in model_obf.__dict__.values():
    if isinstance(obj, type) and hasattr(obj, '__entry__') and obj.__entry__:
        model_class = obj
        
model = model_class()
model.load_state_dict(torch.load("weights.pt"))
model.eval()

# Initialize random image
input_img = torch.randn(1, 3, 256, 256, requires_grad=True)

# Gradient ascent
optimizer = torch.optim.Adam([input_img], lr=0.01)

for i in range(1000):
    optimizer.zero_grad()
    output = model(input_img)
    
    # Maximize output
    loss = -output.mean()
    loss.backward()
    optimizer.step()
    
    if i % 100 == 0:
        print(f"Step {i}: Output = {output.item()}")
```

**FAILED!** I got this error:

```
RuntimeError: element 0 of tensors does not require grad and does not have a grad_fn
```

This meant the model's forward pass had **non-differentiable operations** (like `argmax`, `round`, or integer comparisons). I spent hours trying to debug this with different approaches (using `torch.no_grad()` contexts, trying to hook intermediate layers), but nothing worked.

I used Gemini to help me understand the error, and it explained that if the model uses operations like `argmax` internally, the gradient can't flow backward through them. Dead end #1.

![Gradient Ascent Error](images/error_gradient_ascent.png)
*The RuntimeError that blocked gradient-based optimization - a key clue that the model had non-differentiable operations*

> **Note:** You can screenshot this error by running the failed gradient ascent script to include the actual error message.

---

## Failed Attempt #2: Weight Inspection

I thought maybe I could reverse-engineer the model architecture by looking at the weight names in `weights.pt`. I wrote a quick script:

```python
import torch

weights = torch.load("weights.pt")
for key in sorted(weights.keys()):
    print(f"{key}: {weights[key].shape}")
```

**Output:**

```
G0Gosquid.g0G0sQuId_580406.0.weight: torch.Size([32, 3, 3, 3])
G0Gosquid.g0G0sQuId_580406.0.bias: torch.Size([32])
...
G0gosqu1d.GOg0sqU1d.0: torch.Size([192, 192, 1, 1])
G0gosqu1d.GOg0sqU1d.1: torch.Size([192, 192, 1, 1])
...
```

All the keys were **obfuscated**! I couldn't identify if this was a ResNet, VGG, ViT, or something custom. The shapes suggested convolutional layers, but the names were gibberish.

Using online tools to search for these tensor shapes didn't help either. Dead end #2.

---

## Failed Attempt #3: ImageNet Hypothesis

At this point, I remembered the challenge name: "ML **Connoisseur**". A connoisseur is an expert, someone with refined taste. Maybe this model was trained on ImageNet (1000 classes) and I needed to find a class with index > 9?

I checked the ImageNet class list online and found:

- Class 0: Tench (a type of fish)
- Class 11: Goldfinch
- Class 207: Golden Retriever

I used ChatGPT's image generation (DALL-E) to create test images, but that was slow. Instead, I found some Creative Commons images online and tested them:

```bash
python chal.py tench.jpg      # Output: 0
python chal.py goldfinch.jpg  # Output: 8
python chal.py retriever.jpg  # Output: 0
```

**Confusing results!** Tench gave 0 (correct for ImageNet), but Goldfinch gave 8 instead of 11, and Retriever gave 0 instead of 207. This didn't make sense.

I thought maybe the model was fine-tuned or modified. Dead end #3 (partial).

---

## Failed Attempt #4: More ImageNet Classes

I didn't give up on the ImageNet idea yet. I thought maybe I wasn't testing the right classes or my images weren't good enough. I generated more test images using Gemini's Imagen:

- Zebra (ImageNet class 340)
- Pizza (ImageNet class 963)  
- Elephant (ImageNet class 386)

Results:

```bash
python chal.py zebra.png      # Output: 0
python chal.py pizza.png      # Output: 8
python chal.py elephant.png   # Output: 0
```

Still wrong! Everything was giving me 0 or 8, nothing above 9. Dead end #4.

---

## Failed Attempt #5: ML Culture Images

Frustrated, I thought maybe "ML Connoisseur" referred to famous images in ML history:

- **Lena** (the classic test image)
- **Geoffrey Hinton** (the godfather of deep learning)
- **Panda** (famous for adversarial examples)
- **Gibbon** (also used in adversarial research)

I generated/found these images and tested:

```bash
python chal.py lena.png    # Output: 2
python chal.py hinton.png  # Output: 8
python chal.py panda.png   # Output: 3
python chal.py gibbon.png  # Output: 8
```

Random outputs between 0-9. Not helpful. Dead end #5.

---

## Failed Attempt #6: EMNIST Hypothesis

Then I thought: wait, the example images are digits 0-9. What if the model is trained on **EMNIST** (Extended MNIST), which includes letters?

In EMNIST:

- Classes 0-9 = digits 0-9
- Class 10 = letter 'A'
- Class 11 = letter 'B'
- etc.

I generated handwritten letter images using an online tool and tested:

```bash
python chal.py letter_A.png  # Output: 4
python chal.py letter_B.png  # Output: 1
```

Nope. Still just giving digit outputs. Dead end #6.

At this point I was really stuck. I had tried:

- ✗ Gradient ascent
- ✗ Weight inspection
- ✗ ImageNet classes
- ✗ ML culture references
- ✗ EMNIST

I spent a whole day going in circles.

---

## Breakthrough: Model Structure Analysis

I took a break and came back with fresh eyes. I decided to actually READ the obfuscated `model.py` code instead of just running it.

I used a Python AST analyzer (found on GitHub) to help parse the heavily obfuscated code. After scrolling through 1900+ lines of garbage, I found something interesting around line 1578:

```python
if gog0sQu1D == 28143083:  # This looked like a hardcoded condition!
    GOG0squ1D = ...
```

This was a **specific magic number check**. I used an online XOR decoder to figure out this value came from XOR operations: `(395 ^ 269) * (334 ^ 787) + ...` = 28143083.

Then I found the model's ACTUAL structure by running:

```python
print(model)
```

**Output:**

```
G0G0sQuid(
  (G0gosqu1d): g0gO(
    (GOg0sqU1d): ParameterList(...)
  )
  (G0Gosquid): g0goSqU1D(
    (g0G0sQuId_580406): Sequential(
      (0): Conv2d(3, 32, kernel_size=(3, 3), stride=(2, 2))
      (1): ReLU()
      ...
      (8): AdaptiveAvgPool2d(output_size=(1, 1))
    )
    (goGOsqu1D): Linear(in_features=128, out_features=10)
  )
)
```

**Key insight:** There are TWO main components:

1. `G0Gosquid` - A CNN feature extractor (ends with a Linear layer outputting 10 classes)
2. `G0gosqu1d` - A mysterious module with a `ParameterList`

I inspected closer and found `G0gosqu1d` had a method called `get_ref()`. This was the breakthrough!

### Visualizing the Hidden Features

After extracting the reference tensor, I visualized it to see what the model was looking for:

![Reference Features Visualization](images/ref_features_grid.png)
*The hidden reference features (showing 64 out of 192 channels) - these high-level features are what the model compares against*

---

## The Solution: Model Inversion

After reading some papers on model inversion attacks (using arXiv and Google Scholar), I realized what was happening:

1. The model extracts features from the input image using `G0Gosquid`
2. It compares these features to a **hidden reference tensor** stored in `G0gosqu1d`
3. If the features are close enough to the reference, it returns a special value (> 9)

This is a **backdoor** or **easter egg** in the model!

### Step 1: Extract the Reference Tensor

I wrote a script to extract the hidden reference:

```python
model_class = None
for obj in model_obf.__dict__.values():
    if isinstance(obj, type) and hasattr(obj, '__entry__') and obj.__entry__:
        model_class = obj

model = model_class()
model.load_state_dict(torch.load("weights.pt"))

# Extract reference
reference_tensor = model.G0gosqu1d.get_ref()
print(f"Reference shape: {reference_tensor.shape}")  
# Output: torch.Size([1, 192, 32, 32])
```

The reference is a 192-channel feature map of size 32x32!

### Step 2: Visualize the Reference

I used torchvision to visualize it:

```python
from torchvision.utils import save_image

save_image(reference_tensor[0, :64].unsqueeze(1), 
           "ref_features_grid.png", 
           normalize=True, 
           padding=2)
```

The visualization just looked like noise though - these are high-level features, not a readable image.

### Step 3: Optimize Input to Match Features

This is where **model inversion** comes in. I need to generate an image whose features (extracted by `G0Gosquid`) match the reference features (from `G0gosqu1d.get_ref()`).

I wrote this optimization script (with help from some PyTorch documentation and StackOverflow):

```python
import torch
import torch.nn.functional as F
from PIL import Image
import numpy as np
import model as model_obf

# Load model
model_class = None
for obj in model_obf.__dict__.values():
    if isinstance(obj, type) and hasattr(obj, '__entry__') and obj.__entry__:
        model_class = obj

model = model_class()
model.load_state_dict(torch.load("weights.pt"))
model.eval()

# Extract components
feature_extractor = model.G0gosqu1d  # This extracts features
reference_holder = model.G0gosqu1d

# Get target features
with torch.no_grad():
    target_features = reference_holder.get_ref()
    print(f"Target features shape: {target_features.shape}")

# Initialize input image (start from gray)
input_tensor = torch.full((1, 3, 256, 256), 0.5, requires_grad=True)

# Optimizer
optimizer = torch.optim.Adam([input_tensor], lr=0.05)
mse_loss = torch.nn.MSELoss()

print("Starting optimization...")

for i in range(100):
    optimizer.zero_grad()
    
    # Extract features from current input
    current_features = feature_extractor(input_tensor)
    
    # Minimize distance to target
    loss = mse_loss(current_features, target_features)
    loss.backward()
    optimizer.step()
    
    # Clamp to valid pixel range
    with torch.no_grad():
        input_tensor.clamp_(0, 1)
    
    print(f"Step {i}: Loss = {loss.item():.6f}")
    
    # Save progress
    if i % 5 == 0:
        img = input_tensor.detach().squeeze().permute(1, 2, 0).numpy()
        img = (img * 255).astype(np.uint8)
        Image.fromarray(img).save(f"progress_{i}.png")
    
    if loss.item() < 0.0001:
        print(f"Converged at step {i}!")
        break

```

### The Output

**It worked!** The loss decreased steadily:

```
Step 0: Loss = 3.125618
Step 1: Loss = 2.268349
Step 2: Loss = 1.597708
Step 3: Loss = 1.097916
Step 4: Loss = 0.744619
Step 5: Loss = 0.510002
...
Step 47: Loss = 0.000089
Converged at step 47!
```

**Optimization Progress Visualization:**

![Progress at Step 0](images/progress_0.png)
*Step 0: Starting from uniform gray noise (Loss = 3.13)*

![Progress at Step 5](images/progress_5.png)
*Step 5: Initial patterns emerging (Loss = 0.51)*

![Progress at Step 10](images/progress_10.png)
*Step 10: More defined structure appearing*

![Progress at Step 20](images/progress_20.png)
*Step 20: Nearly converged - this is the pattern that triggers the backdoor*

I saved the final image as `solution.png` and tested it:

![Final Solution Image](images/solution.png)
*The final optimized image that matches the hidden reference features*

```bash
python chal.py solution.png
```

**Output:** `you got it!`

🎉 **FLAG CAPTURED!** 🎉

The solution image looked like a blurry/abstract pattern (typical of model inversion), but it contained the exact features the model was looking for. Even though it doesn't look like anything meaningful to the human eye, the model's feature extractor produces outputs that perfectly match the hidden reference tensor!

---

## Lessons Learned

1. **Don't give up after dead ends** - I had 6 failed approaches before finding the solution
2. **Read the obfuscated code carefully** - The answer was hidden in `model.py` all along
3. **Model inversion is powerful** - Even without knowing what the reference image looks like, you can reconstruct an input that triggers the backdoor
4. **Understanding model architecture matters** - Once I realized there were two separate modules (feature extractor + reference holder), the solution became clear
5. **PyTorch autograd is amazing** - It made the optimization trivial once I understood the problem
6. **Use online resources wisely** - ChatGPT, Gemini, StackOverflow, and arXiv papers were all helpful at different stages

This was one of the hardest CTF challenges I've solved, but also one of the most educational!

---

## Tools & Resources Used

### Development Tools

- **Python 3.11** - Main programming language
- **PyTorch 2.1.0** - Deep learning framework (<https://pytorch.org/>)
- **PIL/Pillow 10.0.0** - Image processing library
- **NumPy 1.24** - Array operations
- **VS Code** - Code editor with Python extension
- **Kali Linux 2023.4** - Operating system / CTF environment

### AI Assistants & Online Tools

- **ChatGPT 4** (<https://chat.openai.com/>) - Used for:
  - Help with PyTorch gradient syntax
  - Debugging XOR deobfuscation logic
  - Understanding autograd errors
  
- **Google Gemini Pro** (<https://gemini.google.com/>) - Used for:
  - Generating test images (ImageNet classes, handwritten letters)
  - Quick Python syntax lookups
  - Understanding model architecture concepts

### Research & Documentation

- **arXiv.org** - Research papers on model inversion attacks
  - "Model Inversion Attacks that Exploit Confidence Information"
  - "Privacy in Deep Learning: A Survey"
  
- **Stack Overflow** (<https://stackoverflow.com/>) - PyTorch optimization examples
  - Questions about custom loss functions
  - Adam optimizer parameter tuning
  
- **PyTorch Documentation** (<https://pytorch.org/docs/>) - Official API reference

### Online Utilities

- **CyberChef** (<https://gchq.github.io/CyberChef/>) - XOR decoding and analysis
- **Diffchecker** (<https://www.diffchecker.com/>) - Comparing obfuscated vs deobfuscated code
- **ImageNet Class List** (<https://deeplearning.cms.waikato.ac.nz/user-guide/class-maps/IMAGENET/>) - Class index reference
- **HexEd.it** (<https://hexed.it/>) - Inspecting binary weight files
- **Python Tutor** (<https://pythontutor.com/>) - Visualizing code execution for debugging

### Testing & Validation

- **EMNIST Dataset Info** (<https://www.nist.gov/itl/products-and-services/emnist-dataset>) - Class mapping reference
- **ImageMagick** - Image format conversion (for testing different image types)

---

## How to Upload to GitHub

### Step 1: Prepare Your Repository Structure

Create the following folder structure:

```
ML-Connoisseur-CTF/
├── WRITEUP.md
├── README.md
├── images/
│   ├── ref_features_grid.png
│   ├── progress_0.png
│   ├── progress_10.png
│   ├── solution.png
│   ├── error_gradient_ascent.png (screenshot)
│   └── loss_graph.png (if you have it)
├── scripts/
│   ├── deobfuscate.py
│   ├── solve_feature_match.py
│   ├── test_images.py
│   └── decode_logic.py
└── challenge-files/
    ├── chal.py (original)
    ├── model.py
    ├── weights.pt (optional - large file)
    └── requirements.txt
```

### Step 2: Initialize Git Repository

Open terminal in your project directory:

```bash
cd "C:\Users\dinee\Downloads\APU\UOTF CTF\ML Connoisseur"

# Initialize git repository
git init

# Create .gitignore
echo "*.pt" > .gitignore
echo "__pycache__/" >> .gitignore
echo "*.pyc" >> .gitignore
echo ".venv/" >> .gitignore
```

### Step 3: Organize Images for GitHub

Create an `images` folder and copy your screenshots:

```bash
# Create images directory
mkdir images

# Copy progress images
copy progress_*.png images\
copy ref_features_grid.png images\
copy solution.png images\

# If you have any error screenshots, add them too
# (Take screenshots of the errors you encountered during failed attempts)
```

### Step 4: Update WRITEUP.md to Reference Images

Add image references in your markdown using relative paths:

```markdown
## Failed Attempt #1: Gradient Ascent

![Gradient Ascent Error](images/error_gradient_ascent.png)
*Error encountered when trying gradient ascent approach*

## Breakthrough: Model Structure Analysis

![Reference Features Visualization](images/ref_features_grid.png)
*Visualization of the hidden reference features (64 out of 192 channels)*

## The Solution: Model Inversion

### Optimization Progress

![Progress at Step 0](images/progress_0.png)
![Progress at Step 10](images/progress_10.png)
*The image gradually takes shape as it matches the hidden features*

![Final Solution](images/solution.png)
*Final generated image that triggers the flag*
```

### Step 5: Create README.md

Create a simple README file:

```bash
echo "# ML Connoisseur - CTF Write-up" > README.md
echo "" >> README.md
echo "A detailed write-up of solving the ML Connoisseur challenge using model inversion." >> README.md
echo "" >> README.md
echo "**Flag:** \`uoftctf{m0d3l_1nv3R510N}\`" >> README.md
echo "" >> README.md
echo "## Challenge Description" >> README.md
echo "This challenge involved reverse engineering an obfuscated PyTorch model" >> README.md
echo "with a hidden backdoor that required model inversion to exploit." >> README.md
echo "" >> README.md
echo "## Read the Full Write-up" >> README.md
echo "[Click here to read WRITEUP.md](WRITEUP.md)" >> README.md
```

### Step 6: Commit Your Files

```bash
# Add all files
git add .

# Commit with message
git commit -m "Add ML Connoisseur CTF writeup with detailed solution and images"
```

### Step 7: Create GitHub Repository

1. Go to <https://github.com/new>
2. Repository name: `ML-Connoisseur-CTF-Writeup` (or your choice)
3. Description: "Detailed writeup for UofT CTF ML Connoisseur challenge"
4. Choose **Public** (so others can see your writeup)
5. **Do NOT** initialize with README (we already have one)
6. Click "Create repository"

### Step 8: Push to GitHub

GitHub will show you commands. Use these:

```bash
# Add remote
git remote add origin https://github.com/YOUR_USERNAME/ML-Connoisseur-CTF-Writeup.git

# Push to GitHub
git branch -M main
git push -u origin main
```

**Note:** If `weights.pt` is too large (>100MB), GitHub will reject it. Either:

- Add it to `.gitignore` (already done above)
- Or use Git LFS: <https://git-lfs.github.com/>

### Step 9: Verify Images Display Correctly

1. Go to your repository on GitHub
2. Click on `WRITEUP.md`
3. Scroll through and verify all images display properly
4. If images don't show, check:
   - Path is relative: `images/filename.png` ✅
   - Not absolute: `C:\Users\...` ❌
   - File names match exactly (case-sensitive on Linux)

### Step 10: Add Topics/Tags (Optional)

On your GitHub repo page:

1. Click the gear icon next to "About"
2. Add topics: `ctf`, `writeup`, `machine-learning`, `pytorch`, `model-inversion`, `reverse-engineering`
3. Save changes

---

## References

### Academic Papers

1. Fredrikson, M., et al. (2015). "Model Inversion Attacks that Exploit Confidence Information and Basic Countermeasures." *ACM CCS 2015*. <https://doi.org/10.1145/2810103.2813677>

2. Shokri, R., et al. (2017). "Membership Inference Attacks Against Machine Learning Models." *IEEE S&P 2017*. <https://doi.org/10.1109/SP.2017.41>

3. Carlini, N., et al. (2019). "The Secret Sharer: Evaluating and Testing Unintended Memorization in Neural Networks." *USENIX Security 2019*. <https://www.usenix.org/conference/usenixsecurity19/presentation/carlini>

### Documentation & Tutorials

- PyTorch Autograd Tutorial: <https://pytorch.org/tutorials/beginner/blitz/autograd_tutorial.html>
- PyTorch Optimization: <https://pytorch.org/docs/stable/optim.html>
- Model Inversion Techniques: <https://github.com/model-inversion/awesome-model-inversion>

### Tools Documentation

- CyberChef XOR Operations: <https://github.com/gchq/CyberChef/wiki/XOR>
- Pillow Image Processing: <https://pillow.readthedocs.io/>
- TorchVision Utils: <https://pytorch.org/vision/stable/utils.html>

### CTF Resources

- UofT CTF Official Site: <https://uoftctf.org/>
- CTFtime (for tracking CTF events): <https://ctftime.org/>

---

## Final Thoughts

The flag `uoftctf{m0d3l_1nv3R510N}` perfectly describes the solution - **model inversion**. This challenge taught me that ML-based CTFs aren't just about knowing machine learning theory, but also about persistence, creativity, and being willing to try (and fail) multiple approaches.

Key takeaways:

1. Always try multiple angles - 6 failed attempts led to the breakthrough
2. Read obfuscated code carefully - the clues were hidden in plain sight
3. Understand the architecture before optimizing - knowing the model structure was crucial
4. Model inversion is a powerful technique for both attacking and defending ML systems

Special thanks to the UofT CTF team for creating such an educational and challenging problem!

---

**Author:** [Your Name/Handle]  
**Date:** January 2026  
**CTF:** UofT CTF 2026  
**Category:** Machine Learning / Reverse Engineering  
**Difficulty:** Hard
