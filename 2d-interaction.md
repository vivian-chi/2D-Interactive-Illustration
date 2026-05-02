PROJECT PRD: Little Girl & Red Balloon (Scroll Experience)
1. Project Overview
A 2D web interactive illustration where a black-and-white line-art girl holds a red balloon.
As the user scrolls down, the balloon floats upward. The girl chases it.
At the very end, she catches the balloon and both fly off the screen together.

Scrolling up reverses the entire animation: they come back down, and she releases the balloon back to the starting position.

2. Visual Style
Element	Specification
Background	White or off-white (#FAFAFA)
Girl & props	Black strokes only, 2–3px line weight, no fill
Balloon	Only colored element — vivid red (#FF3366 or #FF0000)
Style reference	Simpler than Banksy, like clean children's book line art
Canvas size	Responsive, but design based on 800×600 viewport
3. Assets (Illustration Frames)
You already have these. The AI code must support:

Girl frames (7 total)
text
G1: standing, looking up
G2: reaching up on tiptoes
G3: jumping
G4: running (right foot forward)
G5: running (left foot forward)
G6: grabbing balloon (arms up, fingers touching balloon)
G7: flying away (horizontal, hair + dress flowing back)
Balloon frames (3 total)
text
B1: normal circle
B2: slightly squashed (105% width, 95% height)
B3: slightly stretched (95% width, 105% height)
4. Interaction Logic (Scroll)
Scroll Down (Balloon rises)
Scroll %	Balloon Y	Girl Frame	Girl Y	Notes
0%	350px	G1	500px	Starting position
10%	300px	G2	500px	Reaching
20%	250px	G4	490px	Start chase
40%	200px	G5	470px	Running
60%	150px	G4	440px	Running faster
80%	100px	G5	400px	Almost there
90%	60px	G6	380px	Grabbing moment
100%	off screen (Y = -100px)	G7	off screen (Y = -150px)	Fly away together
Scroll Up (Reverse)
Entire process reverses seamlessly

At 90% → 80%: girl releases balloon, frame changes back to G5

At 0%: back to G1 standing

5. Animation Details
Chase Smoothing (Important)
Girl does NOT snap instantly to balloon Y

Girl's Y position lerps toward balloon Y with easing:

text
girl.y += (balloon.y - girl.y) * 0.08
Frame Cycling
Balloon: cycle B1 → B2 → B1 → B3 → B1 (loop every 200ms)

Girl running (G4 ↔ G5): swap every 120ms when scroll is active

Grabbing (G6): single static frame, triggered at 90% scroll

Fly away (G7): static frame, moves off screen

Scroll Speed Influence
Faster scrolling = faster frame switching (min 60ms, max 200ms)

No scroll = frames freeze

6. Technical Requirements
Requirement	Specification
Rendering	HTML5 Canvas 2D (better performance and control than SVG)
Scroll handling	wheel event with preventDefault() to hijack scroll
Or	Hidden tall div + window.scrollY mapping
Responsive	Canvas scales, but Y positions adjust proportionally
Frame rate	60fps with requestAnimationFrame
Asset loading	Preload all images before starting
Fallback	Show "scroll to play" message if no wheel event
7. State Machine (Simplified)
text
STATE_IDLE    (no scroll for 1s)
STATE_RISE    (scrolling down)
STATE_FALL    (scrolling up)  
STATE_GRAB    (at 90%, briefly)
STATE_FLY     (100%, both off screen)
STATE_RETURN  (scrolling up from fly state)
8. Edge Cases & Polish
Case	Behavior
User scrolls past 100%	Stay in FLY state, cannot go further
User scrolls up from FLY	Reverse: girl appears from top, balloon appears, release animation
Very fast scroll	Frame rate caps at 60fps, skip intermediate scroll values gracefully
Window resize	Recalculate all Y positions proportionally
Mobile touch	Use touchmove instead of wheel
9. Emotional / UX Notes for AI
Make the chase feel hopeful but slightly desperate.
When she grabs the balloon (G6), pause scroll response for 0.2 seconds — a tiny "catch" moment.
Then transition to G7 + both flying up.
The scroll-up return should feel gentle, not abrupt.

10. Example Prompt to AI (Short Version)
Build a single HTML/CSS/JS file.
Use canvas. Load 7 girl frames and 3 balloon frames (I will provide image URLs or base64 placeholders).
Implement scroll-controlled animation: balloon rises on scroll down, girl chases with easing.
At 90% scroll, girl grabs balloon (frame G6). At 100%, both girl (frame G7) and balloon fly off screen upward.
Scroll up reverses everything smoothly.
Only balloon is red. Everything else black strokes on white background.
Include frame cycling for idle and running.
Make it 60fps and responsive.