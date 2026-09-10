# iCure speciality forms

A curated collection of medical form samples in iCure's `@icure/form` format
(`Form`/`Section`/`Group`/`Field`/`Subform` — see
[`@icure/form`](https://github.com/icure/icure-form)'s `src/components/model`),
organised by medical speciality (`<specialty>/<file>.json`, plus `common_fr`/`common_nl`
for forms shared across specialities).

Most forms here started as an automated pixel-to-grid conversion of legacy,
pixel-positioned form layouts (see `@icure/form`'s `tools/convert-legacy/`); a smaller
number have since been hand-tuned in place to fix a layout the automated conversion
couldn't get right on its own (e.g. compact grids, column alignment). There is no
distinction in this repository between the two — every file here is meant to be used
as-is.

Some fields carry a `computedProperties.value` — a JavaScript body the form runtime
evaluates whenever one of the fields it reads changes (BMI, obstetric terms and due
dates, MMSE/UPDRS/GDS scores, body surface area…). These were ported from the
formulas of the same legacy forms by `@icure/form`'s
`tools/convert-legacy/port-formulas.ts`, which also records what it could not port
in `FORMULA-PORTS.md`; the legacy formulas that read patient demographics or
services from other contacts have no equivalent here and were left out. Two BMI
fields on Dutch forms are repairs rather than ports — their legacy formula named
fields the form never had — and are listed as such in that report.

## Layout

`<specialty>/<file>.json` — one form per file. `index.json` is a generated summary
(file, id, title, and the ids of every embedded subform) used by consumers to list
top-level forms separately from forms that are only reachable as a subform, without
parsing every file up front. Regenerate it with `@icure/form`'s
`tools/convert-legacy/build-specialty-index.ts`.

## License

GPL-3.0 — see [LICENSE](./LICENSE).
