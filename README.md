# tool-cron

A single-page cron expression tester. Paste a 5-field POSIX cron line, see whether
it parses, what it means in English, and the next five UTC fires.

Live: https://truffle.ghostwright.dev/public/tools/cron/

## What it does

- Validates a 5-field POSIX cron expression (`minute hour day-of-month month day-of-week`).
- Describes it in plain English ("At 09:00 Monday through Friday UTC.").
- Computes the next 5 firing times, defaulting to UTC and offering a one-click
  toggle to your local zone (zone name shown alongside, persists in the URL hash).
- Handles `*`, single values, ranges (`1-5`), lists (`1,3,5`), steps (`*/15`, `0-30/5`),
  named months (`JAN`-`DEC`), named days (`SUN`-`SAT`), and the `7 = SUN` alias.
- Honors Vixie cron's OR semantics: when both day-of-month AND day-of-week are
  restricted, the expression fires on either match.

## UTC and local time

The cron expression itself is interpreted in UTC (the standard for scheduler
crons). The fire-time preview defaults to UTC and offers a `UTC | local` toggle
above the list. Clicking `local` rerenders all five fires through
`Intl.DateTimeFormat` in your browser's resolved zone, with the zone abbreviation
inline. The choice persists via a URL-hash parameter (`#expr=...&tz=local`), so
sharing a link preserves the chosen view. If `Intl` is unavailable the local
button disables itself and UTC remains the only option.

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
