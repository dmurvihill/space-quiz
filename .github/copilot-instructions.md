# Copilot instructions

## Project structure and architecture

The project is a single-file, dependency-free web app. `index.html` contains the page structure, CSS theme and responsive behavior, the ten-question quiz dataset, and the JavaScript that drives the intro, question flow, answer feedback, score/progress, and results screen. There is no build step or separate application layer; keep changes self-contained unless the project grows beyond this structure.

Quiz content is data-driven in the `questions` array. Each entry has a category, question, four options, a zero-based correct `answer` index, and a historical explanation in `fact`. `renderQuestion()` draws the current entry, `chooseAnswer()` locks and evaluates the selected answer, and `showResults()` selects the end-screen reaction by score.

## Commands and verification

There is no package manifest, build system, or configured test/lint command. Open `index.html` directly in a browser (`file://`) to run the app; it does not require a server or dependencies.

For a manual smoke test, start and finish a quiz in a browser. Check keyboard access to the start, answer, next, and restart buttons; verify that correct answers increment the score and show green feedback, incorrect answers preserve the score and reveal the right answer with red feedback, progress advances, and the results screen shows the final score and reaction. Check both light and dark system color preferences if changing theme styles.

## Codebase conventions

- Keep question wording, distractors, answer index, and explanatory fact together in the corresponding `questions` entry. The answer index must match the option order.
- Keep the quiz flow in the existing `renderQuestion()`, `chooseAnswer()`, `showResults()`, and `startQuiz()` functions; update progress, score, feedback, and focus as part of the relevant state transition.
- Use native `<button>` elements for actions and answers. The app intentionally transfers keyboard focus to the first answer on each new question, to Next after an answer, and to the results heading at completion. Preserve this focus flow and the existing live regions when changing interactions.
- Theme colors are CSS custom properties. The outer page follows `prefers-color-scheme`; `.card` intentionally overrides those properties for its dark command-center theme. Preserve text contrast for normal, correct, and incorrect states.
- Animations honor `prefers-reduced-motion`; keep that accommodation for any new motion effects.
