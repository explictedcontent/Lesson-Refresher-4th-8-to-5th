# Summer Refresher Course — Project Memory

## What this is
Interactive summer review course for a 4th-grader going into 5th grade.
Standalone HTML lessons, no dependencies. Hosted via GitHub Pages on the `main` branch.
Dev branch: `claude/art-lesson-refresher-rqz9ib`

## EVERY lesson MUST auto-save
All 4 of these event listeners are required in every lesson:
```javascript
document.addEventListener('visibilitychange', () => { if (document.visibilityState === 'hidden') saveAll(); });
window.addEventListener('pagehide', saveAll);
window.addEventListener('beforeunload', saveAll);
window.addEventListener('blur', saveAll);
```
Also: quiz answers save immediately on each answer (`ansQ()` writes to QAKEY), and writing pads use a 300ms debounce save.

## Standard storage keys per lesson (exact names matter)
```
QAKEY = "<subject>-l<N>-qans"   // mid-quiz saves (per-answer)
QKEY  = "<subject>-l<N>-quiz"   // final score
WKEY  = "<subject>-l<N>-writing" // writing pad
```
Cross-lesson review tab key: `refresher-mistakes` (shared, never cleared unless user clears)

## logMistake pattern (exact — required in every lesson)
```javascript
function logMistake(correct, questionText, quizTitle) {
  try {
    let m = JSON.parse(localStorage.getItem('refresher-mistakes') || '{}');
    const key = 'Subject|Day N: Topic|' + quizTitle;
    if (!correct) {
      m[key] = { subject: 'Subject', day: 'Day N', q: questionText, file: 'lesson-file.html' };
    } else { delete m[key]; }
    localStorage.setItem('refresher-mistakes', JSON.stringify(m));
  } catch(e) {}
}
```

## Quiz fairness rule (CRITICAL)
In every multiple-choice quiz, the CORRECT answer must NOT be the longest option — a 10-yo exploited "just pick the longest one." Balance option lengths (make 1-2 distractors as long or longer than the correct answer) and vary which option is longest across questions. Numeric/short-value options are exempt. Applies to any choice-based game too (e.g. scenario pickers), not just the graded quiz. ALSO vary the correct answer's POSITION across A/B/C/D — never put the correct answer at the same index for every question (a fixed position is just as exploitable as a fixed length).

## Quiz pattern (required order)
`buildQuiz()` first, then `restoreQuiz()` — both called at init. Never reversed.

## CSS variables (same in every lesson)
```
--bg:#14151d; --panel:#1e2130; --panel2:#252a3a; --ink:#f4f5fb;
--muted:#a7adc4; --accent:#ff7a59; --accent2:#5bd1c4; --good:#7bd88f;
--warn:#ffd166; --bad:#ff6b81; --line:#2e3347
```

## Math design rule (CRITICAL)
Sea turtle / animal data appears ONLY in word problem TEXT.
Math games, tools, and mechanics use CLEAN NUMBERS — no animals in the calculation UI.

## Coding lessons — "Boss the Panda" game style
- No "lesson", "phase", or "quiz" language visible on screen
- XP counter fixed top-right, mission language, game copy throughout
- EVERY coding level ends with a **🧪 CODE LAB** tab (added as the final mission,
  screen `sc7`/`tab7`): 5 tap-to-order code puzzles where the kid assembles a real
  program line-by-line, with trap lines to leave out. This exists because the build/quiz
  screens tap through in ~5–10 min; the Lab adds hands-on, think-required time on task.
  Engine is a self-contained IIFE (no top-level globals except `window.__lab`/`renderLab`),
  reads `window.LAB_CFG` (key `coding-l<N>-lab`), reuses the lesson's `addXP`, logs to
  `refresher-mistakes`, and saves on the same visibilitychange/pagehide/beforeunload/blur
  events. Source of truth for puzzles + the inserter: scratchpad `lab-data.js` /
  `insert-lab.js` / `lab-engine.html`. (Note: lesson 08 was missing its closing
  `</script></body></html>` — repaired.)
- Level 1 (`coding-lesson-01-intro.html`): variables, if/else, loops, grid challenge
- Level 2 (`coding-lesson-02-functions.html`): define functions, call them, parameters, return values
- Level 3 (`coding-lesson-03-lists.html`): lists/arrays — build, index access, loop, push/pop
- Level 4 (`coding-lesson-04-random.html`): random numbers — dice, fairness, crits, boss fight
- Level 5 (`coding-lesson-05-objects.html`): objects/properties — build a character sheet, read/change stats, squad of objects
- Level 6 (`coding-lesson-06-build-a-game.html`): CAPSTONE — build a real playable arcade game (Bamboo Catcher) piece by piece, then play it. Most interactive yet.
- Level 7 (`coding-lesson-07-pixel-art.html`): build a real pixel-art drawing app (grid/nested loops, palette list, tap events, tool functions), then draw & save art. Creative build.
- Level 8 (`coding-lesson-08-timers.html`): build a timer-based reaction game (Target Smash) — setInterval timers, countdown, random spawns, tap events, score. Then play it.
- Level 9 (`coding-lesson-09-sound.html`): build a music maker (Panda Beats) — Web Audio tones/frequencies, note list, 2D beat grid, timer-driven playback loop. Then compose & play.
- Level 10 (`coding-lesson-10-maze.html`): build a maze game (Maze Runner) — row/col coordinates, grid data, collision detection, win check; move/build/solve. Then play it.
- Level 11 (`coding-lesson-11-story.html`): build a Mad Libs Story Machine — strings/text, concatenation with +, inputs, templates; generate silly personalized stories.
- Level 12 (`coding-lesson-12-adventure.html`): build a Choose-Your-Own-Adventure — scenes as objects, choices as if/else branches, multiple endings; author your own ending, then play to find them all.
- Level 13 (`coding-lesson-13-pet.html`): build a virtual pet (Panda Pal) — object stats, care-action functions, setInterval decay (state over time), if-statement mood; keep it thriving.
- Level 14 (`coding-lesson-14-flyer.html`): build a tap-to-fly physics game (Sky Glider) — gravity+velocity each frame, flap sets speed up, cloud collision, scoring; then play it.
- Level 15 (`coding-lesson-15-realcode.html`): **NEW "type real code" style** (parent asked for real coding, not tap-to-order). Kid TYPES actual JavaScript into an editor (`right()`/`left()`/`up()`/`down()`/`say()`, for-loops, variables, nested loops, own functions) and the panda runs it on a grid, harvesting bamboo. User code executes in a **Web Worker** (blob URL) terminated after 1.5s (endless-loop guard) that collects an action list the main thread animates; friendly kid-facing error messages; +25 XP/mission; autosaves typed code (`coding-l15-code`) + XP (`coding-l15-xp`). Works inside the all-in-one srcdoc iframe (Worker + localStorage both OK). `coding-real-demo.html` is the gentler warm-up (move-only). This is the model to convert Levels 1–14 to when asked — based on MakeCode/Minecraft "type code → it happens on screen."
- Level 16 (`coding-lesson-16-painter.html`): type-real-code, **Panda Painter**. `paint("red")` colors the current square; kid matches a GOAL canvas shown beside their own. Teaches: commands that take an **input/argument**, loops, variables holding **words** (`let color = "yellow"`, then `paint(color)` — no quotes), moving to a second row, and **your own function with a parameter** (`function stripe(c)`). Same Worker sandbox + 1.5s guard; colors limited to red/blue/green/yellow/purple/white; targeted friendly errors (e.g. `paint(red)` without quotes → "Colors are words, so they need quotes").
- Level 17 (`coding-lesson-17-decisions.html`): type-real-code, **Panda Decides** — if/else. Adds `blocked()`, which returns **true/false** for "is the square to my RIGHT a wall or the edge?". Ramp: see true/false with `say(blocked())` → `if` → `if/else` → decision **inside a loop** (staircase) → wrap the decision in your own `stepSmart()` function. IMPORTANT: because `blocked()` depends on live position, the **Worker simulates the world** (receives grid/start/walls, tracks x/y, validates moves) and returns the panda's position after each move; the page just replays them. Console APPENDS the result so `say()` output stays visible.
- Level 18 (`coding-lesson-18-while.html`): type-real-code, **Panda Keeps Going** — **while loops**. Adds `gems()`, which returns a **number** (how many collected so far), so the Worker now tracks collected gems as well as position. Ramp: `say(gems())` shows a number → comparisons (`<`/`>`) give true/false → `while (gems() < 4)` → while + if/else so you **don't have to count the steps** → wrap it in your own `stepSmart()`. The 600-step cap doubles as the runaway-`while` lesson ("does the thing it waits for ever become false?").
- **TEACHING STANDARD for all future coding levels** (parent feedback: an adult couldn't follow the old nested-loop/`%` mission, so the kid was just tapping through): ONE new idea per mission; a plain-English **🧠 teach card** BEFORE any code explaining what it means, with a small annotated example; `//` comments inside the starter code; NO unexplained tricks (no `%`, no nested loops for beginners); and some missions ship **intentionally incomplete** so the kid must read/count/fix rather than just press RUN. Missions must be solvable exactly as the teach card describes — verify each intended solution actually wins.

## Day themes (completed)
- Day 2: Red Panda 🐾
- Day 3: Snow Leopard 🐆
- Day 4: Giant Panda 🐼
- Day 5: Sea Turtle 🐢
- Day 6: Octopus 🐙
- Day 7: Axolotl 🦎
- Day 8: Peregrine Falcon 🦅
- Day 9: Emperor Penguin 🐧
- Day 10: Honeybee 🐝
- Day 11: Bat 🦇
- Day 12: Chameleon 🦎
- Day 13: Dolphin 🐬
- Day 14: Elephant 🐘
- Day 15: Kangaroo 🦘
- Day 16: Polar Bear 🐻‍❄️
- Day 17: Sky Bison 🦬💨 (Avatar-themed; real flight science & real cultures behind the Four Nations)
- Day 18: Gray Wolf 🐺 (real Yellowstone trophic cascade; wolves in world cultures; ELA similes/metaphors; Math decimals)
- Day 19: Nine-Tailed Fox 🦊🔥 (Naruto-themed; REAL fox science + real kitsune/huli jing/kumiho folklore & Japan geography; ELA main idea & details; Math volume)
- Day 20: Dragon 🐉 (real animals behind the legend — Komodo/Draco/bombardier beetle + science self-correction; dragons across China/Wales/Indonesia; ELA making inferences; Math order of operations)
- Day 21: Phoenix 🔥🦅 (REAL fire ecology — serotinous cones, fire-follower woodpecker, succession + a balanced wildfire-danger/safety section; firebird legends across Egypt/Greece/China/Russia/Japan + Silk Road; ELA summarizing; Math factors/multiples/primes)

## All-in-one build
Script: `/tmp/claude-.../scratchpad/build-allinone.js`
Run with: `node build-allinone.js` from the scratchpad dir
Output: `Fourth-to-5th-Refresh-All-In-One.html` (currently 4881KB, 114 lessons)
Each lesson is inlined into `window.LESSONS[file]` and opened in a **srcdoc iframe**
(`frame.srcdoc = window.LESSONS[file]`). This is REQUIRED for saving to work:
every lesson declares the same top-level names (`const QAKEY`, `let xp`, `function go`…),
so injecting all their scripts into ONE page throws "Identifier 'QAKEY' has already been
declared" on the 2nd lesson opened — that lesson never initializes and its 4 auto-save
listeners never attach ("not saving" bug). A srcdoc iframe gives each lesson its own
document/script scope (no collisions) while sharing the parent origin, so localStorage
saving works and persists. Do NOT go back to appending lesson `<script>`s into the hub page.

## Committing
Branch: `claude/art-lesson-refresher-rqz9ib`
Always: `git push -u origin claude/art-lesson-refresher-rqz9ib`
