# Copilot instructions

## Project shape

- `space-quiz.html` is the complete application: semantic HTML, all styles, quiz data, and interaction logic are kept in one file.
- There are no package manifests or external runtime dependencies. Open the HTML file directly in a browser; no server or build step is required.

## Architecture and conventions

- The `questions` array is the source of truth for quiz content. Each entry has a question string, four answer strings, a zero-based `correct` answer index, and a short explanatory `fact`.
- `renderQuestion()` rebuilds the answer buttons from the current question. `chooseAnswer()` locks choices, updates the score only on correct answers, marks the correct and selected answers, and announces explanatory feedback. The next button advances or displays the final result.
- Progress represents completed questions: it advances when moving to the next question and reaches the total on the results screen. Keep the text label and `role="progressbar"` values in sync with that behavior.
- Theme colors are CSS custom properties defined on `:root` and overridden by `:root[data-theme="dark"]`. `setTheme()` updates the root attribute and theme-color metadata; the saved preference falls back to the system preference when storage is unavailable.
- Keep presentation rules in the inline `<style>` block and app behavior in the inline `<script>`. The design uses responsive CSS and honors `prefers-reduced-motion`.
- Preserve accessible interaction patterns: use native buttons for actions and answers, live regions for changing score/feedback/results, and move focus to the new question after advancing and to the restart button at completion. Decorative emoji and display elements should remain hidden from assistive technology where marked `aria-hidden`.
- When rendering question content, build elements with DOM APIs and assign user-facing strings with `textContent`; do not turn quiz data into markup.

## Build, test, and lint

- There are no build, test, or lint commands configured in this project.
- Verify UI changes by opening `space-quiz.html` in the integrated browser. Exercise a correct and incorrect answer, confirm score and progress, advance through the results screen, restart, and check both themes and keyboard focus.
