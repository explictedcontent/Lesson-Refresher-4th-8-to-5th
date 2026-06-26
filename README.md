# ☀️ Summer Refresher Course · 4th → 5th Grade

A self-paced summer course to keep skills sharp for next school year — a mix of
4th-grade review plus a head start on 5th. Every lesson is an interactive page
that runs right in the browser: tap to answer or draw, a timer paces the lesson,
and **everything saves automatically on the device** (drawings, your place, and
any quiz questions answered wrong).

**👉 Open [`index.html`](index.html) — one app with a tab for each subject. Pick a
subject, tap a lesson, and go. Wrong quiz answers collect on the _Review_ tab and
clear themselves once they're answered correctly.**

---

## 🎨 Art — 8 interactive lessons

**Elements of Art**

| # | Lesson | File |
| :-: | ----- | ---- |
| 1 | Color Mixing | [art-lesson-01-color-mixing.html](art-lesson-01-color-mixing.html) |
| 2 | Warm & Cool Colors | [art-lesson-02-warm-cool-colors.html](art-lesson-02-warm-cool-colors.html) |
| 3 | Value — Light & Shadow | [art-lesson-03-value-light-shadow.html](art-lesson-03-value-light-shadow.html) |
| 4 | Line | [art-lesson-04-line.html](art-lesson-04-line.html) |
| 5 | Shape & Form | [art-lesson-05-shape-form.html](art-lesson-05-shape-form.html) |
| 6 | Texture | [art-lesson-06-texture.html](art-lesson-06-texture.html) |
| 7 | Space | [art-lesson-07-space.html](art-lesson-07-space.html) |

**Principles of Art**

| # | Lesson | File |
| :-: | ----- | ---- |
| 8 | Balance | [art-lesson-08-balance.html](art-lesson-08-balance.html) |

*More principles (Pattern, Contrast, Emphasis, Proportion, Rhythm, Unity) are on the way.
Written lesson-plan notes for the full sequence live in [`art-lessons/`](art-lessons/).*

## 🔢 Math — 4 interactive lessons

| # | Lesson | File |
| :-: | ----- | ---- |
| 1 | Place Value | [math-lesson-01-place-value.html](math-lesson-01-place-value.html) |
| 2 | Comparing & Ordering | [math-lesson-02-comparing-ordering.html](math-lesson-02-comparing-ordering.html) |
| 3 | Rounding | [math-lesson-03-rounding.html](math-lesson-03-rounding.html) |
| 4 | Adding & Subtracting | [math-lesson-04-add-subtract.html](math-lesson-04-add-subtract.html) |

## 🔬 Science — 2 interactive lessons

| # | Lesson | File |
| :-: | ----- | ---- |
| 1 | The World of Science | [science-lessons/science-lesson-1.html](science-lessons/science-lesson-1.html) |
| 2 | Earth, Life & Forces | [science-lessons/science-lesson-2.html](science-lessons/science-lesson-2.html) |

## 🌎 Social Studies — 3 interactive lessons

| # | Lesson | File |
| :-: | ----- | ---- |
| 1 | U.S. Geography | [social-lesson-01-us-geography.html](social-lesson-01-us-geography.html) |
| 2 | Native American Cultures | [social-lesson-02-native-americans.html](social-lesson-02-native-americans.html) |
| 3 | The 3 Branches of Government | [social-lesson-03-government.html](social-lesson-03-government.html) |

---

### ➕ Adding a subject or lesson
Drop the lesson's `.html` file into the repo (or a subject folder), then register it in the
`SUBJECTS` array near the top of [`index.html`](index.html) — copy an existing entry, change the
title/emoji/description and the `file:` path. The card, tab, and Review wiring all follow
automatically.

### 📱 Make it clickable on any phone/tablet
Turn on **GitHub Pages** (Settings → Pages → Deploy from a branch → `Main` → `/root`). That
publishes [`index.html`](index.html) at a web address you can bookmark and share — no downloads,
no folders, and the in-app lesson view + saved progress work fully.
