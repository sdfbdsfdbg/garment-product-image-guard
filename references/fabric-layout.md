# Fixed Fabric Detail Layout

Read this file before planning, prompting, generating, or verifying `SKU_08_fabric.jpg`.

## Reference Assets

Inspect both approved references before generation:

- `../assets/fabric-layout-reference-01.jpg`
- `../assets/fabric-layout-reference-02.jpg`

Use them as the binding layout, hierarchy, spacing, and quality standard. Never copy their garment, color, composition, texture, icons, logo, or wording into another SKU.

## Mandatory Canvas And Split

- Default to a landscape 3:2 canvas unless the user or sales platform explicitly requires another aspect ratio.
- Keep the same structure at every aspect ratio: a clean left information column occupying about 25-30% of the width and one dominant fabric macro occupying about 70-75% on the right.
- Do not reverse the columns, turn the layout into a square central poster, scatter text over the macro, or use multiple competing fabric crops.
- Keep the left background white or very light neutral with restrained black, charcoal, or SKU-coordinated accent color.

## Mandatory Left-Column Order

Use this fixed top-to-bottom order:

1. Title `面料细节`.
2. Optional one-line material/hand-feel subtitle only when directly supported by source evidence or clearly visible structure.
3. Composition block only when composition is confirmed from the same SKU input.
4. Fabric-characteristics rows.
5. One clean full-garment thumbnail at the bottom.

Do not change this order.

## Composition Rule

- Inspect all SKU input images for a readable hang tag, wash label, certificate, neck label, fabric label, barcode tag, or care card.
- When confirmed, show heading `面料成分` and reproduce the exact fiber names, percentages, shell/lining/rib distinctions, and source wording without inference or simplification.
- When not confirmed, omit the entire composition block, including the `面料成分` heading. Move the characteristics and thumbnail upward to use the space.
- Never write guessed composition, fiber names, percentages, `成分未知`, `暂无数据`, `以实物为准`, or another placeholder.

## Fabric Characteristics

- Use 2-4 concise rows beneath the composition area, with restrained simple line icons when useful.
- Every row must be supported by visible source evidence or a confirmed label.
- Prefer directly auditable descriptions such as `纹理清晰`, `细密针织`, `平滑梭织`, `罗纹清晰`, `光泽细腻`, `花型清晰`, `轻薄半透明`, or `自然垂顺` only when the source visibly proves them.
- Do not claim `柔软亲肤`, `透气舒适`, `吸湿排汗`, `抗皱`, `保暖`, `凉感`, `防晒`, `防水`, performance, function, or comfort without explicit source evidence.
- Use fewer rows rather than inventing a characteristic.

## Garment Thumbnail

- Place one clean full-garment thumbnail below the characteristics in the lower part of the left column.
- Use the accepted AI-generated front white image as the primary rendering reference.
- Preserve exact category, silhouette, length, color, pattern, logo/print, collar, sleeves, closure, pockets, waist, belt/tie, and hem.
- Keep the thumbnail large enough to identify the SKU but subordinate to the right-side macro.
- No hanger, clip, mannequin, model, watermark, unrelated logo, or source-photo background.

## Right-Side Fabric Macro

- Fill the right area with one sharp photoreal near-distance fabric view from the exact SKU.
- Match source color, weave or knit, yarn scale, pattern or check scale, stripe spacing, print repeat, sheen, thickness, transparency, lining visibility, drape, and fold behavior.
- Use the strongest source fabric closeup as binding evidence; if absent, use a source body detail plus the accepted front white image.
- The macro must look like the garment's real fabric, not generic stock cloth or a different textile.
- Do not place composition text, characteristics, icons, or the garment thumbnail over the macro.

## Required Prompt Block

Include all of the following in every fabric prompt:

- Exact layout lock: left 25-30% information column, right 70-75% single macro.
- Exact left-column order and exact approved Chinese copy.
- Composition status, exact display text, and evidence filename, or `composition block omitted`.
- Source-supported characteristic rows and their evidence.
- Accepted front-white filename for the garment thumbnail.
- Fabric macro evidence filename and exact color/texture/pattern/transparency locks.
- Negative constraints for unsupported composition, unsupported claims, wrong thumbnail, generic stock texture, reversed columns, and layout drift.

## Verification

Reject and regenerate if any condition is true:

- The layout is not a left information column plus a dominant right macro.
- The left column is outside the approximate 25-30% width range or the macro is not visually dominant.
- The left-column order differs from title, optional subtitle, confirmed composition, characteristics, and garment thumbnail.
- Confirmed composition is omitted, altered, mistranslated, or placed outside the composition block.
- Unconfirmed composition is guessed or replaced with a placeholder.
- A characteristic lacks source evidence or makes an unsupported comfort or performance claim.
- The garment thumbnail is missing, too small to identify, or inconsistent with the exact SKU.
- The macro uses the wrong color, weave/knit, pattern scale, sheen, thickness, transparency, drape, or fold behavior.
- Text, icons, or the thumbnail intrude into the right macro area.
- The result looks like a generic fabric advertisement instead of documentation of the exact SKU.
