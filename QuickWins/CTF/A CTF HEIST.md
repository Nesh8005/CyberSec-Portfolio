# ML CONNOISSEUR: A CTF HEIST

**A Story-Driven Presentation Script for 4 People**

*Runtime: 15-20 minutes*  
*Theme: Tech Thriller / Hacker Drama*

---

## CHARACTER ASSIGNMENTS

**ALEX (The Lead / Optimist)** - Main narrator, idealistic, never gives up  
**JORDAN (The Skeptic / Pragmatist)** - Questions everything, realistic, brings team back to earth  
**RILEY (The Researcher / Theorist)** - Deep diver, loves reading papers, brings academic insights  
**MORGAN (The Wildcard / Coder)** - Gets hands dirty with code, spontaneous, breakthrough thinker  

---

## PROPS & SETUP

**Physical Props:**

- 4 laptops (or fake laptops with printouts)
- Whiteboard/projector showing: code snippets, error messages, progress images
- Coffee cups (visual gag - they get increasingly tired)
- Printed "FAILED" stamps/signs to hold up dramatically

**Digital Props (Slides):**

- Slide 1: Challenge description
- Slide 2-7: Each failed attempt with images
- Slide 8: The breakthrough (reference features image)
- Slide 9-12: The solution process
- Slide 13: Final flag reveal

---

## ACT 1: THE CHALLENGE (3 minutes)

### SCENE 1: THE BRIEFING

*[Lights up. All 4 team members enter from different sides, looking excited but nervous. They meet at center stage. ALEX holds a printout.]*

**ALEX:**  
*(enthusiastically)*  
Alright team, we've got 48 hours to crack the "ML Connoisseur" challenge. First place gets major bragging rights AND goes on our resumes.

**JORDAN:**  
*(scrolling on laptop, skeptical)*  
"ML Connoisseur"? Sounds pretentious. What does it even do?

**MORGAN:**  
*(quickly types, reads screen)*  
It's a digit classifier. Feed it an image of 0 through 9, it tells you what number it is.

**RILEY:**  
*(adjusting glasses, reading documentation)*  
But here's the catch - we need to make it output a number GREATER than 9. Which shouldn't be possible for a digit classifier.

**ALEX:**  
Unless...

**ALL TOGETHER:**  
*(turning to audience)*  
There's a backdoor.

*[Dramatic pause. Thunder sound effect (optional).]*

**JORDAN:**  
Great. A backdoor in 1900 lines of obfuscated PyTorch code. What could possibly go wrong?

---

### SCENE 2: DEOBFUSCATION

*[MORGAN moves to center, typing frantically. Others gather around.]*

**MORGAN:**  
First problem - the main script is completely obfuscated. Look at this mess.

*[Projects slide showing obfuscated XOR code.]*

**RILEY:**  
*(leaning in)*  
Those are XOR operations. Classic obfuscation technique. If we can find the key...

**MORGAN:**  
Already on it. Testing all 256 possible keys...  
*(dramatic pause, typing)*  
Got it! Key is 42.

**ALEX:**  
*(laughs)*  
42. The answer to life, the universe, and hacking CTF challenges.

*[Projects deobfuscated code.]*

**JORDAN:**  
*(reading)*  
So the flag triggers when the model outputs greater than 9. Simple enough.  
*(pause)*  
Too simple.

**ALEX:**  
*(determined)*  
Let's try the obvious approach first. Gradient ascent!

---

## ACT 2: THE FAILURES (8 minutes)

*[Montage music begins - something like "Eye of the Tiger" but nerdier. Team moves in coordinated choreography between "attempts."]*

### ATTEMPT 1: GRADIENT ASCENT DISASTER

**ALEX:**  
*(confidently typing)*  
If we use activation maximization, we can generate an image that maximizes the output!

**MORGAN:**  
*(coding frantically)*  
Setting up the optimizer... Adam, learning rate 0.01... backward pass... and...

*[Loud ERROR sound. Red screen flashes.]*

**ALL:**  
*(reading error in unison)*  
"RuntimeError: element 0 of tensors does not require grad and does not have a grad_fn"

**RILEY:**  
*(explaining to audience)*  
Translation: the model has non-differentiable operations. ArgMax, integer comparisons... gradient can't flow backward.

**JORDAN:**  
*(holding up "FAILED #1" sign)*  
Dead end number one.

*[ALEX slumps. MORGAN pats shoulder encouragingly.]*

---

### ATTEMPT 2: WEIGHT INSPECTION

**RILEY:**  
*(stepping forward with laptop)*  
Maybe we can reverse-engineer the architecture by examining the weight file.

*[Projects weight keys on screen.]*

**RILEY:**  
Let's see... "G0Gosquid.g0G0sQuId_580406"... "GOg0sqU1d.ParameterList"...

**JORDAN:**  
*(squinting)*  
Is that... is that even English?

**MORGAN:**  
It's obfuscated variable names. Could be a ResNet, VGG, or something completely custom.

**ALEX:**  
*(searching on laptop)*  
I'm searching these tensor shapes online...  
*(pause)*  
Nothing. Absolutely nothing.

**RILEY:**  
*(holding up "FAILED #2" sign)*  
Dead end number two.

---

### ATTEMPT 3-5: THE MONTAGE OF FAILURE

*[Quick-fire sequence. Each person takes a failed attempt. Coffee cups multiply on stage.]*

**JORDAN:**  
*(holding ImageNet class list)*  
ATTEMPT 3: Maybe it's trained on ImageNet! Testing goldfinch... class 11...  
*(checks output)*  
Output: 8.  
*(to camera)*  
Not 11. Failed.

**MORGAN:**  
*(holding picture of Lena)*  
ATTEMPT 4: ML culture references! The famous Lena image... Geoffrey Hinton's face...  
*(checks laptop)*  
Random outputs. Failed.

**RILEY:**  
*(holding EMNIST dataset paper)*  
ATTEMPT 5: Extended MNIST with letters! 'A' should be class 10...  
*(types, checks)*  
Output: 4.  
*(sighs)*  
Failed.

**ALEX:**  
*(standing, looking defeated)*  
That's 5 dead ends. We've tried everything.

**JORDAN:**  
*(checking watch)*  
And we're 36 hours in with nothing to show.

---

### THE DARK MOMENT

*[Team sits in dejected circle. Lights dim slightly. Quiet moment.]*

**RILEY:**  
Maybe it's impossible.

**MORGAN:**  
Maybe we're missing something obvious.

**JORDAN:**  
Maybe we should just submit a writeup of our failures and call it a learning experience.

**ALEX:**  
*(standing up slowly)*  
No. We're not giving up.  
*(intensely)*  
We haven't actually READ the model code. We've been running it, testing it, but not READING it.

**MORGAN:**  
It's 1900 lines of garbage!

**ALEX:**  
Then let's read 1900 lines of garbage.

---

## ACT 3: THE BREAKTHROUGH (5 minutes)

### SCENE 3: THE EUREKA MOMENT

*[ALEX sits at laptop. Others watch skeptically. Time-lapse effect - ALEX scrolls, squints, types, scrolls more. Others bring coffee, check phones.]*

**ALEX:**  
*(suddenly)*  
Wait. WAIT.  
*(louder)*  
**WAIT!**

*[Everyone jumps up.]*

**JORDAN:**  
What? What did you find?

**ALEX:**  
*(pointing at screen)*  
Line 1578. There's a hardcoded condition:  
"if gog0sQu1D == 28143083"

**RILEY:**  
A magic number check! That's a backdoor trigger!

**MORGAN:**  
But we don't know what that number represents.

**ALEX:**  
*(typing)*  
Let me print the model structure...

*[Projects model architecture on screen.]*

**ALEX:**  
Look! Two modules:  

- G0Gosquid: A normal CNN feature extractor  
- G0gosqu1d: A mysterious ParameterList...  
*(gasps)*  
With a method called "get_ref()"!

**RILEY:**  
*(excited, standing up)*  
Get reference! It's storing a reference tensor!

**MORGAN:**  
So the model isn't just classifying...

**JORDAN:**  
*(realizing)*  
It's COMPARING input features to a hidden reference!

**ALL:**  
*(turning to audience)*  
**Model inversion!**

---

### SCENE 4: THE SOLUTION

**RILEY:**  
*(pulls out academic paper)*  
I've read about this! Model inversion attacks from Fredrikson et al. If we extract the reference features and optimize an input to match them—

**MORGAN:**  
*(already typing)*  
Way ahead of you. Extracting reference tensor now...

*[Projects reference features grid image.]*

**JORDAN:**  
*(looking at image)*  
That's... noise?

**RILEY:**  
High-level features. Not human-readable, but perfect for optimization.

**ALEX:**  
*(taking over laptop)*  
Morgan, set up an Adam optimizer. Learning rate 0.05. We'll start from a gray image and minimize MSE loss between our features and the reference.

**MORGAN:**  
*(typing rapidly)*  
Loss function ready. Input tensor initialized. Starting optimization...

*[Projects screen showing loss decreasing.]*

**MORGAN:**  
Step 0: Loss = 3.12  
Step 1: Loss = 2.26  
Step 5: Loss = 0.51...

**JORDAN:**  
It's working!

**RILEY:**  
*(showing progress images)*  
Look - the image is taking shape!

*[Projects progression: progress_0, progress_5, progress_10, progress_20.]*

**ALEX:**  
*(watching intently)*  
Come on... come on...

**MORGAN:**  
Step 47: Loss = 0.000089  
CONVERGED!

---

### SCENE 5: THE FLAG REVEAL

*[Dramatic pause. All team members gather around MORGAN's laptop.]*

**MORGAN:**  
*(typing)*  
Running the test...  
`python chal.py solution.png`

*[Pause. Screen shows thinking/loading animation.]*

**SCREEN:**  

```
you got it!
```

**JORDAN:**  
*(disbelieving)*  
No way.

**RILEY:**  
*(checking)*  
The flag is...

**ALEX:**  
*(reading)*  
uoftctf{m0d3l_1nv3R510N}

**ALL:**  
*(celebrating, high-fiving)*  
**YES!!!**

**MORGAN:**  
*(to audience)*  
Model inversion. The flag was literally telling us the solution the whole time!

---

## ACT 4: THE LESSON (2 minutes)

*[Team moves to front of stage, addressing audience directly.]*

**ALEX:**  
So what did we learn from 48 hours of failure and one moment of triumph?

**JORDAN:**  
Never give up after dead ends. We had SIX failed attempts - gradient ascent, weight inspection, ImageNet, ML culture, EMNIST, and more ImageNet.

**RILEY:**  
Read the code, not just run it. The answer was hidden in plain sight in line 1578.

**MORGAN:**  
Model inversion is powerful. We reconstructed the exact input needed without ever seeing the original reference image.

**ALEX:**  
And most importantly...  
*(turning to team)*  
Teamwork. Each of us brought something different:

**JORDAN:**  
Skepticism kept us grounded.

**RILEY:**  
Research gave us the academic foundation.

**MORGAN:**  
Coding skills made it real.

**ALEX:**  
And persistence got us to the finish line.

---

### FINALE

**ALL:**  
*(to audience)*  
In CTF challenges - and in real cybersecurity - the impossible is just...

**ALEX:**  
An optimization problem.

**JORDAN:**  
With the right approach.

**RILEY:**  
The right research.

**MORGAN:**  
And the right team.

**ALL:**  
Thank you!

*[Team takes a bow. Fade to black.]*

---

## PRODUCTION NOTES

### Timing Breakdown

- Act 1 (The Challenge): 3 min
- Act 2 (The Failures): 8 min  
- Act 3 (The Breakthrough): 5 min
- Act 4 (The Lesson): 2 min  
- **Total: ~18 minutes**

### Technical Requirements

1. **Projector/Screen** - Essential for showing code, errors, images
2. **Sound Effects** - Error beeps, success chimes (optional but adds drama)
3. **Lighting** - Dim for "dark moment," brighten for breakthrough
4. **Props** - Laptops, coffee cups, printed "FAILED" signs

### Tips for Distinction-Level Performance

1. **Memorize, Don't Read**  
   - Know your lines cold
   - Make eye contact with audience
   - Be natural, not robotic

2. **Physical Acting**  
   - Use the stage - move around
   - React to each other's discoveries
   - Show frustration, excitement, relief

3. **Timing & Pacing**  
   - Don't rush technical explanations
   - Build dramatic tension before reveals
   - Pause for laughs (there are comedic moments)

4. **Audience Engagement**  
   - Make eye contact
   - Explain jargon simply
   - Show, don't just tell (use the images!)

5. **Technical Accuracy**  
   - Know your technical content
   - Be ready for Q&A after
   - Have backup slides with more detail

6. **Team Chemistry**  
   - Play off each other's energy
   - Support scene partners
   - High-five/celebrate together authentically

### Customization Options

**Make it Funnier:**  

- Add more coffee-drinking gags
- Have JORDAN make sarcastic comments about error messages
- MORGAN can rage-type during frustrating moments

**Make it More Technical:**  

- Add a "chalk talk" moment where RILEY explains model inversion on whiteboard
- Show actual code snippets during montage
- Include a "hacking montage" with Matrix-style visuals

**Make it More Dramatic:**  

- Add a countdown clock (48 hours → 24 → 12 → etc.)
- Rival team subplot (another team is also trying to solve it)
- Stakes: "If we don't solve this, we fail the course!"

### Costume Suggestions

- **ALEX:** Hoodie, confident hacker vibe
- **JORDAN:** Business casual, pragmatic look  
- **RILEY:** Glasses, academic/researcher style
- **MORGAN:** Band t-shirt, chaotic coder energy

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
