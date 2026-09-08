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

## Layout

`<specialty>/<file>.json` — one form per file. `index.json` is a generated summary
(file, id, title, and the ids of every embedded subform) used by consumers to list
top-level forms separately from forms that are only reachable as a subform, without
parsing every file up front. Regenerate it with `@icure/form`'s
`tools/convert-legacy/build-specialty-index.ts`.

## License

GPL-3.0 — see [LICENSE](./LICENSE).
