# Lab 9 - JavaScript Error Handling, Monitoring, & JS Docs

Live site: **https://howardguan24.github.io/Lab9_Starter/**
(Enable GitHub Pages on `main` / root in the repo settings to publish.)

## What this lab demonstrates

### Step 2 - Console API buttons
Each button in the `#error-btns` section is wired to a different `console`
method. Open DevTools → Console and try them in this order to see the
indented group, the timer, etc., behave correctly:

| Button | Method |
| --- | --- |
| Console Log | `console.log` |
| Console Error | `console.error` |
| Console Count | `console.count` |
| Console Warn | `console.warn` |
| Console Assert | `console.assert` (fires because we pass `false`) |
| Console Clear | `console.clear` |
| Console Dir | `console.dir` of a DOM node |
| Console dirxml | `console.dirxml` of a DOM node |
| Console Group Start / End | `console.group` + `console.groupEnd` |
| Console Table | `console.table` of an array of objects |
| Start / End Timer | `console.time('lab9-timer')` + `console.timeEnd` |
| Console Trace | `console.trace` from a nested call |

### Step 3 - try / catch / finally
The Error Calculator validates its inputs and wraps the math in
`try / catch / finally`. Triggers:

- Leave a field blank or type letters → throws `CalculatorError`.
- Pick `/` with the second value `0` → throws `CalculatorError`
  ("Cannot divide by zero").
- The `finally` block logs a timestamp on every submit, success or fail.

### Step 4 - throw + custom Error type
`CalculatorError extends Error` lives at the top of the inline `<script>`.
Inside the catch we use `instanceof CalculatorError` to give the user a
friendly message, and re-`throw` anything we don't recognize so the
global handler still sees it.

### Step 5 - Global error handler + TrackJS
Three global hooks are installed:

- `window.onerror` (classic API)
- `window.addEventListener('error', ...)` (modern equivalent)
- `window.addEventListener('unhandledrejection', ...)` (for promises)

The **"Trigger a Global Error"** button calls a function that does not
exist. Because the click handler does **not** wrap it in try/catch,
the `ReferenceError` escapes to all three handlers above (and to
TrackJS).

#### TrackJS setup
The TrackJS agent script and install token are already wired into
`index.html`. To capture errors:

1. Open the published GitHub Pages site (link above).
2. Click "Trigger a Global Error" a few times. The calculator error
   cases (blank input, divide by zero, etc.) also report up.
3. Open https://my.trackjs.com and confirm the errors are listed.
4. Screenshot the dashboard with your username + error list visible
   and commit it to this repo as `trackjs-screenshot.png`.

## File layout

- `index.html` - all the markup, styles, and JS for the lab.
- `favicon.ico` - leftover from starter, harmless.
- `trackjs-screenshot.png` - your TrackJS dashboard screenshot (add it).
