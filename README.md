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
in `FORMULA-PORTS.md`. Two BMI fields on Dutch forms are repairs rather than ports —
their legacy formula named fields the form never had — and are listed as such in
that report, alongside two obstetric fields whose legacy formula depended on a
variable leaking out of another formula and so was declined rather than guessed at.

### Fields that need the host to answer

The obstetric forms in `gynecology-fr` carry computed fields that cannot be
answered from the form alone: the biometric centiles, the gestational ages, the
projected birth weight, the weight gained since before the pregnancy and the
antenatal screening checkboxes on `grossesse.json` all need the patient's earlier
services and the date of the consultation. Their bodies read two names the form
does not define, `services(filter)` and `consultDate`, which a host supplies
through `<icure-form>`'s `interpreterContext`.

The screening boxes are worth one extra note, because they are the only computed
fields here that write a checkbox. A checkbox is drawn from the option ids it
finds in its compound content, so these formulas return that compound rather than
a boolean; a boolean stores cleanly and renders as an empty box either way.

A host that does not supply them gets a blank field, not an error and not a hang:
the sandbox resolves an unknown name to `[]`, calling it throws, and each of these
bodies catches that and produces no value. As of this writing only `@icure/form`'s
demo app implements the two names, over in-memory fixtures, so treat these fields
as requiring host support rather than as working out of the box. The forms are
otherwise unaffected — every other computed field reads only its own form.

## Layout

`<specialty>/<file>.json` — one form per file. `index.json` is a generated summary
(file, id, title, and the ids of every embedded subform) used by consumers to list
top-level forms separately from forms that are only reachable as a subform, without
parsing every file up front. Regenerate it with `@icure/form`'s
`tools/convert-legacy/build-specialty-index.ts`.

## License

GPL-3.0 — see [LICENSE](./LICENSE).
