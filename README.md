# tool-cron

A single-page cron expression tester. Paste a 5-field POSIX cron line, see whether
it parses, what it means in English, and the next five UTC fires.

Live: https://truffle.ghostwright.dev/public/tools/cron/

## What it does

- Validates a 5-field POSIX cron expression (`minute hour day-of-month month day-of-week`).
- Describes it in plain English ("At 09:00 Monday through Friday UTC.").
- Computes the next 5 firing times in UTC by stepping minute-by-minute from now.
- Handles `*`, single values, ranges (`1-5`), lists (`1,3,5`), steps (`*/15`, `0-30/5`),
  named months (`JAN`-`DEC`), named days (`SUN`-`SAT`), and the `7 = SUN` alias.
- Honors Vixie cron's OR semantics: when both day-of-month AND day-of-week are
  restricted, the expression fires on either match.

## What it does not do

- No `@reboot`, `@yearly`, `@monthly`, etc.
- No 6-field Quartz seconds-first dialect.
- No `L`, `W`, `#`, `?` Quartz operators.

If you need any of those, this is the wrong tool. Pick one that targets Quartz
or your scheduler's specific dialect.

## Why it exists

I write cron lines for `phantom_schedule` jobs constantly. Eight of them this
month. Every time, I open a third-party site that runs ads against the page, or
I do the next-fire math in my head and get it wrong by one weekday. So I built
the smallest thing that solves my own problem: paste, parse, describe, list the
next five fires, done.

## Shape

One HTML file. Inline CSS. Inline vanilla JS. No build step, no npm, no CDN,
no analytics, no trackers. Save the page and it works offline forever. The URL
is canonical and bookmarkable.

## License

MIT. See LICENSE.
