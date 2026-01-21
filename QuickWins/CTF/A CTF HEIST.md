# ML CONNOISSEUR: A CTF HEIST

**A Story-Driven Presentation Script for 4 People**

*Runtime: 15-20 minutes*  
*Theme: Tech Thriller / Hacker Drama*

---

## CHARACTER ASSIGNMENTS

**ALEX (The Lead / Optimist)** - Main narrator, idealistic, never gives up  

**DINEESH (The Skeptic / Pragmatist)** - Questions everything, realistic, brings team back to earth  

**SASWIN (The Researcher / Theorist)** - Deep diver, loves reading papers, brings academic insights  

**XINTONG (The Wildcard / Coder)** - Gets hands dirty with code, spontaneous, breakthrough thinker  

---

## PROPS & SETUP

### Physical Props

- 4 laptops (or fake laptops with printouts)
- Whiteboard/projector showing: code snippets, error messages, progress images
- Coffee cups (visual gag - they get increasingly tired)
- Printed "FAILED" stamps/signs to hold up dramatically

### Digital Slides with Images

- **Slide 1:** Title + Challenge description
- **Slide 2:** Deobfuscated code snippet
- **Slide 3:** Failed Attempt #1 - ![Gradient Error](https://raw.githubusercontent.com/Nesh8005/CyberSec-Portfolio/main/QuickWins/CTF/error_gradient_ascent.png)
- **Slide 4:** Failed Attempts #2-5 montage
- **Slide 5:** The Breakthrough - Model architecture diagram
- **Slide 6:** Reference Features - ![Reference](https://raw.githubusercontent.com/Nesh8005/CyberSec-Portfolio/main/QuickWins/CTF/ref_features_grid.png)
- **Slide 7:** Progress Step 0 - ![Progress 0](https://raw.githubusercontent.com/Nesh8005/CyberSec-Portfolio/main/QuickWins/CTF/progress_0.png)
- **Slide 8:** Progress Step 5 - ![Progress 5](https://raw.githubusercontent.com/Nesh8005/CyberSec-Portfolio/main/QuickWins/CTF/progress_5.png)
- **Slide 9:** Progress Step 10 - ![Progress 10](https://raw.githubusercontent.com/Nesh8005/CyberSec-Portfolio/main/QuickWins/CTF/progress_10.png)
- **Slide 10:** Progress Step 20 - ![Progress 20](https://raw.githubusercontent.com/Nesh8005/CyberSec-Portfolio/main/QuickWins/CTF/progress_20.png)
- **Slide 11:** Final Solution - ![Solution](https://raw.githubusercontent.com/Nesh8005/CyberSec-Portfolio/main/QuickWins/CTF/solution.png)
- **Slide 12:** Flag Reveal (animated)
- **Slide 13:** Lessons Learned

---
---

# ACT 1: THE CHALLENGE (3 minutes)

---

## SCENE 1: THE BRIEFING

*[Lights up. All 4 team members enter from different sides, looking excited but nervous. They meet at center stage. ALEX holds a printout.]*

<br>

**ALEX:**  
*(enthusiastically)*  
Alright team, we've got 48 hours to crack the "ML Connoisseur" challenge. First place gets major bragging rights AND goes on our resumes.

<br>

**DINEESH:**  
*(scrolling on laptop, skeptical)*  
"ML Connoisseur"? Sounds pretentious. What does it even do?

<br>

**XINTONG:**  
*(quickly types, reads screen)*  
It's a digit classifier. Feed it an image of 0 through 9, it tells you what number it is.

<br>

**SASWIN:**  
*(adjusting glasses, reading documentation)*  
But here's the catch - we need to make it output a number GREATER than 9. Which shouldn't be possible for a digit classifier.

<br>

**ALEX:**  
Unless...

<br>

**ALL TOGETHER:**  
*(turning to audience)*  
There's a backdoor.

<br>

*[Dramatic pause. Thunder sound effect (optional).]*

<br>

**DINEESH:**  
Great. A backdoor in 1900 lines of obfuscated PyTorch code. What could possibly go wrong?

---

## SCENE 2: DEOBFUSCATION

*[XINTONG moves to center, typing frantically. Others gather around.]*

<br>

**XINTONG:**  
First problem - the main script is completely obfuscated. Look at this mess.

*[Projects slide showing obfuscated XOR code.]*

<br>

**SASWIN:**  
*(leaning in)*  
Those are XOR operations. Classic obfuscation technique. If we can find the key...

<br>

**XINTONG:**  
Already on it. Testing all 256 possible keys...  
*(dramatic pause, typing)*  
Got it! Key is 42.

<br>

**ALEX:**  
*(laughs)*  
42. The answer to life, the universe, and hacking CTF challenges.

*[Projects deobfuscated code.]*

<br>

**DINEESH:**  
*(reading)*  
So the flag triggers when the model outputs greater than 9. Simple enough.  
*(pause)*  
Too simple.

<br>

**ALEX:**  
*(determined)*  
Let's try the obvious approach first. Gradient ascent!

---
---

# ACT 2: THE FAILURES (8 minutes)

*[Montage music begins - something like "Eye of the Tiger" but nerdier. Team moves in coordinated choreography between "attempts."]*

---

## ATTEMPT 1: GRADIENT ASCENT DISASTER

**ALEX:**  
*(confidently typing)*  
If we use activation maximization, we can generate an image that maximizes the output!

<br>

**XINTONG:**  
*(coding frantically)*  
Setting up the optimizer... Adam, learning rate 0.01... backward pass... and...

<br>

*[Loud ERROR sound. Red screen flashes.]*

*[Projects slide with error screenshot]*

<br>

**ALL:**  
*(reading error in unison)*  
"RuntimeError: element 0 of tensors does not require grad and does not have a grad_fn"

<br>

**SASWIN:**  
*(explaining to audience)*  
Translation: the model has non-differentiable operations. ArgMax, integer comparisons... gradient can't flow backward.

<br>

**DINEESH:**  
*(holding up "FAILED #1" sign)*  
Dead end number one.

<br>

*[ALEX slumps. XINTONG pats shoulder encouragingly.]*

---

## ATTEMPT 2: WEIGHT INSPECTION

**SASWIN:**  
*(stepping forward with laptop)*  
Maybe we can reverse-engineer the architecture by examining the weight file.

*[Projects weight keys on screen.]*

<br>

**SASWIN:**  
Let's see... "G0Gosquid.g0G0sQuId_580406"... "GOg0sqU1d.ParameterList"...

<br>

**DINEESH:**  
*(squinting)*  
Is that... is that even English?

<br>

**XINTONG:**  
It's obfuscated variable names. Could be a ResNet, VGG, or something completely custom.

<br>

**ALEX:**  
*(searching on laptop)*  
I'm searching these tensor shapes online...  
*(pause)*  
Nothing. Absolutely nothing.

<br>

**SASWIN:**  
*(holding up "FAILED #2" sign)*  
Dead end number two.

---

## ATTEMPT 3-5: THE MONTAGE OF FAILURE

*[Quick-fire sequence. Each person takes a failed attempt. Coffee cups multiply on stage.]*

<br>

**DINEESH:**  
*(holding ImageNet class list)*  
ATTEMPT 3: Maybe it's trained on ImageNet! Testing goldfinch... class 11...  
*(checks output)*  
Output: 8.  
*(to camera)*  
Not 11. Failed.

<br>

**XINTONG:**  
*(holding picture of Lena)*  
ATTEMPT 4: ML culture references! The famous Lena image... Geoffrey Hinton's face...  
*(checks laptop)*  
Random outputs. Failed.

<br>

**SASWIN:**  
*(holding EMNIST dataset paper)*  
ATTEMPT 5: Extended MNIST with letters! 'A' should be class 10...  
*(types, checks)*  
Output: 4.  
*(sighs)*  
Failed.

<br>

**ALEX:**  
*(standing, looking defeated)*  
That's 5 dead ends. We've tried everything.

<br>

**DINEESH:**  
*(checking watch)*  
And we're 36 hours in with nothing to show.

---

## THE DARK MOMENT

*[Team sits in dejected circle. Lights dim slightly. Quiet moment.]*

<br>

**SASWIN:**  
Maybe it's impossible.

<br>

**XINTONG:**  
Maybe we're missing something obvious.

<br>

**DINEESH:**  
Maybe we should just submit a writeup of our failures and call it a learning experience.

<br>

**ALEX:**  
*(standing up slowly)*  
No. We're not giving up.  
*(intensely)*  
We haven't actually READ the model code. We've been running it, testing it, but not READING it.

<br>

**XINTONG:**  
It's 1900 lines of garbage!

<br>

**ALEX:**  
Then let's read 1900 lines of garbage.

---
---

# ACT 3: THE BREAKTHROUGH (5 minutes)

---

## SCENE 3: THE EUREKA MOMENT

*[ALEX sits at laptop. Others watch skeptically. Time-lapse effect - ALEX scrolls, squints, types, scrolls more. Others bring coffee, check phones.]*

<br>

**ALEX:**  
*(suddenly)*  
Wait. WAIT.  
*(louder)*  
**WAIT!**

<br>

*[Everyone jumps up.]*

<br>

**DINEESH:**  
What? What did you find?

<br>

**ALEX:**  
*(pointing at screen)*  
Line 1578. There's a hardcoded condition:  
"if gog0sQu1D == 28143083"

<br>

**SASWIN:**  
A magic number check! That's a backdoor trigger!

<br>

**XINTONG:**  
But we don't know what that number represents.

<br>

**ALEX:**  
*(typing)*  
Let me print the model structure...

*[Projects model architecture on screen.]*

<br>

**ALEX:**  
Look! Two modules:  

- G0Gosquid: A normal CNN feature extractor  
- G0gosqu1d: A mysterious ParameterList...  
*(gasps)*  
With a method called "get_ref()"!

<br>

**SASWIN:**  
*(excited, standing up)*  
Get reference! It's storing a reference tensor!

<br>

**XINTONG:**  
So the model isn't just classifying...

<br>

**DINEESH:**  
*(realizing)*  
It's COMPARING input features to a hidden reference!

<br>

**ALL:**  
*(turning to audience)*  
**Model inversion!**

---

## SCENE 4: THE SOLUTION

**SASWIN:**  
*(pulls out academic paper)*  
I've read about this! Model inversion attacks from Fredrikson et al. If we extract the reference features and optimize an input to match them—

<br>

**XINTONG:**  
*(already typing)*  
Way ahead of you. Extracting reference tensor now...

<br>

*[Projects reference features grid image - Slide 6.]*

<br>

**DINEESH:**  
*(looking at image)*  
That's... noise?

<br>

**SASWIN:**  
High-level features. Not human-readable, but perfect for optimization.

<br>

**ALEX:**  
*(taking over laptop)*  
Xintong, set up an Adam optimizer. Learning rate 0.05. We'll start from a gray image and minimize MSE loss between our features and the reference.

<br>

**XINTONG:**  
*(typing rapidly)*  
Loss function ready. Input tensor initialized. Starting optimization...

<br>

*[Projects screen showing loss decreasing. Show Slides 7-10 as optimization progresses.]*

<br>

**XINTONG:**  
Step 0: Loss = 3.12  
*(Shows Slide 7: Progress 0)*

Step 1: Loss = 2.26  

Step 5: Loss = 0.51...  
*(Shows Slide 8: Progress 5)*

<br>

**DINEESH:**  
It's working!

<br>

**SASWIN:**  
*(showing progress images)*  
Look - the image is taking shape!

<br>

*[Projects progression: Slides 9 (progress_10) and 10 (progress_20).]*

<br>

**ALEX:**  
*(watching intently)*  
Come on... come on...

<br>

**XINTONG:**  
Step 47: Loss = 0.000089  
CONVERGED!

---

## SCENE 5: THE FLAG REVEAL

*[Dramatic pause. All team members gather around XINTONG's laptop.]*

<br>

**XINTONG:**  
*(typing)*  
Running the test...  
`python chal.py solution.png`

<br>

*[Pause. Screen shows thinking/loading animation. Projects Slide 11: Final solution image.]*

<br>

**SCREEN:**  

```
you got it!
```

<br>

**DINEESH:**  
*(disbelieving)*  
No way.

<br>

**SASWIN:**  
*(checking)*  
The flag is...

<br>

**ALEX:**  
*(reading)*  
uoftctf{m0d3l_1nv3R510N}

<br>

*[Projects Slide 12: Flag reveal with animation.]*

<br>

**ALL:**  
*(celebrating, high-fiving)*  
**YES!!!**

<br>

**XINTONG:**  
*(to audience)*  
Model inversion. The flag was literally telling us the solution the whole time!

---
---

# ACT 4: THE LESSON (2 minutes)

*[Team moves to front of stage, addressing audience directly. Projects Slide 13: Lessons Learned.]*

<br>

**ALEX:**  
So what did we learn from 48 hours of failure and one moment of triumph?

<br>

**DINEESH:**  
Never give up after dead ends. We had SIX failed attempts - gradient ascent, weight inspection, ImageNet, ML culture, EMNIST, and more ImageNet.

<br>

**SASWIN:**  
Read the code, not just run it. The answer was hidden in plain sight in line 1578.

<br>

**XINTONG:**  
Model inversion is powerful. We reconstructed the exact input needed without ever seeing the original reference image.

<br>

**ALEX:**  
And most importantly...  
*(turning to team)*  
Teamwork. Each of us brought something different:

<br>

**DINEESH:**  
Skepticism kept us grounded.

<br>

**SASWIN:**  
Research gave us the academic foundation.

<br>

**XINTONG:**  
Coding skills made it real.

<br>

**ALEX:**  
And persistence got us to the finish line.

---

## FINALE

**ALL:**  
*(to audience)*  
In CTF challenges - and in real cybersecurity - the impossible is just...

<br>

**ALEX:**  
An optimization problem.

<br>

**DINEESH:**  
With the right approach.

<br>

**SASWIN:**  
The right research.

<br>

**XINTONG:**  
And the right team.

<br>

**ALL:**  
Thank you!

<br>

*[Team takes a bow. Fade to black.]*

---
---

# PRODUCTION NOTES

## Timing Breakdown

- **Act 1** (The Challenge): 3 min
- **Act 2** (The Failures): 8 min  
- **Act 3** (The Breakthrough): 5 min
- **Act 4** (The Lesson): 2 min  
- **Total: ~18 minutes**

---

## Technical Requirements

### 1. Projector/Screen

Essential for showing code, errors, images

### 2. Sound Effects (Optional)

- Error beeps
- Success chimes
- Background music for montages

### 3. Lighting

- Dim for "dark moment"
- Brighten for breakthrough

### 4. Props

- Laptops
- Coffee cups
- Printed "FAILED" signs

---

## Tips for Distinction-Level Performance

### 1. Memorize, Don't Read

- Know your lines cold
- Make eye contact with audience
- Be natural, not robotic

### 2. Physical Acting

- Use the stage - move around
- React to each other's discoveries
- Show frustration, excitement, relief

### 3. Timing & Pacing

- Don't rush technical explanations
- Build dramatic tension before reveals
- Pause for laughs (there are comedic moments)

### 4. Audience Engagement

- Make eye contact
- Explain jargon simply
- Show, don't just tell (use the images!)

### 5. Technical Accuracy

- Know your technical content
- Be ready for Q&A after
- Have backup slides with more detail

### 6. Team Chemistry

- Play off each other's energy
- Support scene partners
- High-five/celebrate together authentically

---

## Customization Options

### Make it Funnier

- Add more coffee-drinking gags
- Have DINEESH make sarcastic comments about error messages
- XINTONG can rage-type during frustrating moments

### Make it More Technical

- Add a "chalk talk" moment where SASWIN explains model inversion on whiteboard
- Show actual code snippets during montage
- Include a "hacking montage" with Matrix-style visuals

### Make it More Dramatic

- Add a countdown clock (48 hours → 24 → 12 → etc.)
- Rival team subplot (another team is also trying to solve it)
- Stakes: "If we don't solve this, we fail the course!"

---

## Costume Suggestions

- **ALEX:** Hoodie, confident hacker vibe
- **DINEESH:** Business casual, pragmatic look  
- **SASWIN:** Glasses, academic/researcher style
- **XINTONG:** Band t-shirt, chaotic coder energy

---

## REHEARSAL CHECKLIST

- [ ] All actors have memorized their lines
- [ ] Slides are prepared and tested
- [ ] Props are gathered
- [ ] Sound effects cued up (if using)
- [ ] Blocking (stage movement) planned
- [ ] Run-through with full tech
- [ ] Backup plan for tech failures
- [ ] Q&A prep (know your CTF inside-out)
- [ ] Celebration choreography practiced

---

## BONUS: INTERACTIVE ELEMENTS

### Audience Poll (Optional)

Before Act 2, ask audience:  
*"Quick poll - who here has tried gradient descent for image generation?"*  
Builds connection.

### Live Demo (If Brave)

During Act 3, actually run the optimization live on stage (risky but impressive).

### Post-Presentation Q&A Hooks

- "Want to see the actual code?"
- "Anyone interested in trying ML CTF challenges?"
- "We can show you the full write-up!"

---

**Break a leg! 🎭**

*Remember: You're not just presenting a technical solution - you're telling the story of a journey. Make them feel your frustration, your breakthroughs, and your triumph!*
