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
- Level 1 (`coding-lesson-01-intro.html`): variables, if/else, loops, grid challenge
- Level 2 (`coding-lesson-02-functions.html`): define functions, call them, parameters, return values

## Day themes (completed)
- Day 2: Red Panda 🐾
- Day 3: Snow Leopard 🐆
- Day 4: Giant Panda 🐼
- Day 5: Sea Turtle 🐢

## All-in-one build
Script: `/tmp/claude-.../scratchpad/build-allinone.js`
Run with: `node build-allinone.js` from the scratchpad dir
Output: `Fourth-to-5th-Refresh-All-In-One.html` (currently 1398KB, 38 lessons)
Uses inline injection (not iframe) for iOS Safari compatibility.

## Committing
Branch: `claude/art-lesson-refresher-rqz9ib`
Always: `git push -u origin claude/art-lesson-refresher-rqz9ib`
