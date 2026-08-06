# Four-Grid Lifestyle Collage

Read this file before planning, prompting, generating, or verifying `SKU_05_four_grid.jpg`.

## Reference Assets

Inspect these three approved reference images before generation:

- `../assets/four-grid-reference-01.jpg`: menswear collage with coastal walk, city street, outdoor leisure, and cafe scenes; wide central white copy band.
- `../assets/four-grid-reference-02.jpg`: womenswear collage with coast, lakeside garden, cafe, and flower garden scenes; elegant central headline overlay.
- `../assets/four-grid-reference-03.jpg`: menswear collage with mountain travel, city street, forest path, and cafe scenes; compact central white title label.

Use the assets only for composition, scene variety, typography restraint, lighting, and premium ecommerce mood. Never copy their garments, garment colors, models, logos, accessories, props, or exact locations into a SKU output.

## Required Composition

- Generate a square 2-by-2 collage as one fresh generative-AI output.
- Use four cinematic fashion photographs with cohesive color grading and thin clean white dividers.
- Use the mandatory five-block copy layout in every output: exactly one restrained central headline/subline block plus exactly one title/subline block inside each of the four panels.
- The central block must sit at or near the four-panel crossing as either a narrow white title band or a compact central label. It must be visually centered, clearly separated from the panel copy, and must not cover garment facts.
- Place each panel's copy block in a consistent corner or clean negative-space area within that panel. Do not omit, merge, duplicate, or move a panel copy block into another panel.
- Use four compatible but distinct real-life scenes selected through `scene_context_lock` and [scene-context.md](scene-context.md). Adult scenes may include coast, urban street, garden, cafe exterior, courtyard, architecture, forest path, or outdoor leisure. Childrenswear scenes must follow the child rules below.
- Keep the result premium and natural; do not use white-studio panels.
- Do not locally assemble, crop, paste, or composite four separate images into the required output.

## Same-SKU Lock

- Show the exact same source SKU in all four panels.
- Apply the complete `PROMPT_LOCK_BLOCK` to every panel.
- Preserve color, pattern, real print/logo, collar, sleeves, closure, pockets, belt/tie, hem, silhouette, length, proportions, and fabric behavior in every panel.
- Treat each panel as an independent same-SKU verification target.
- Keep the garment auditable. Standing panels must show enough of the garment to verify silhouette and hem.
- The seated pose must not fold, crop, cover, or distort identity-critical construction.
- Do not tuck, roll, open, layer over, or rest hands or props across locked garment details.

## Model Identity And Pose Lock

- Use four visibly different white European/Western model identities.
- Make facial structure, features, hairstyle, hair color, and overall appearance clearly distinct.
- Do not reuse one identity, create near-duplicates, or simulate difference only through hairstyle, pose, camera angle, clothing accessories, or lighting.
- Match every model to the garment's adult/child and menswear/womenswear context.
- For childrenswear, use at least three panels from amusement park, school campus, playground, sports field, park, children's library, children's museum, or supervised activity-space categories. Do not use cafes, coffee shops, business/commuting settings, luxury lobbies, nightlife, dating, or other adult social scenes.
- Require all four models to be visibly white European/Western people.
- Reject the image if any panel contains a Black or other non-white model. Do not use ambiguous identity descriptions such as `Western`, `international`, `diverse`, or `mixed`; state `white European/Western` in every panel identity lock.
- Keep all four faces visible, sharp, and unobstructed.
- Use exactly four different poses: exactly three standing poses and exactly one seated pose.
- Differentiate body orientation, arm placement, leg placement, gaze direction, and weight distribution.
- Do not count mirrored, slightly shifted, or camera-angle-only variations as different poses.

## Outfit Styling Lock

- Use four visibly different complete outfits while keeping the source SKU itself identical as the hero product in every panel.
- Outfit difference means the models wear different companion apparel around the hero SKU to demonstrate different use cases. It does not mean changing the hero SKU, changing only the model, changing only color, or changing only pose.
- Record concrete `companion_garments`, `footwear_or_legwear`, and `scene_use_case` entries for every panel in `four_grid_plan`.
- For tops, vary the companion bottom category and footwear in every panel, such as jeans, tailored trousers, a skirt, and relaxed denim.
- For shorts, trousers, or skirts, vary the companion top category and footwear in every panel while keeping the SKU waistband, closure, pockets, belt, and hem visible.
- For outerwear, vary the inner top, bottom, and footwear while keeping the complete outerwear SKU visible and preserving its source-supported open/closed state.
- For dresses and rompers, vary visible legwear and footwear in every panel; use clearly different companion combinations such as ankle socks with low-top sneakers, knee socks with loafers, sheer tights with ankle boots, and stockings with low block heels.
- Keep any required lining or underlayer for a sheer garment consistent with source evidence. Do not use underlayer variation to fake a different garment.
- Do not add an outer layer over a top, dress, or romper merely to create variation when it would cover the hero SKU. Do not use a belt, scarf, bag, hat, sunglasses, jewelry, or handheld prop as a substitute for companion-apparel variation.
- Do not tuck, roll, open, knot, layer over, or cover the source SKU. A companion top may be neatly tucked only when the source SKU is a bottom and tucking is necessary to keep its waistband visible.
- Match each outfit to a distinct truthful, age-appropriate scene use case. Adult examples include relaxed casual, urban street, smart commuting, or weekend travel. Child examples include park play, campus activity, playground movement, family outing, or reading/art time.
- Reject near-duplicate outfits that differ only by color, camera angle, hairstyle, or an invisible shoe change.

## Chinese Copy

- Render concise, correct Simplified Chinese.
- Render exactly five visually distinct copy blocks: one central block and four panel blocks. Any other count fails verification.
- The central block is mandatory and contains one 6-14 character headline plus one short truthful subline.
- Every panel block is mandatory and contains one 2-6 character scene title plus one truthful 4-8 character subline.
- Keep panel copy placement consistent across all four panels, using the same alignment, type hierarchy, spacing, and margin logic.
- Use restrained black, charcoal, gray, or white typography according to contrast, with generous spacing and no decorative text effects.
- Keep all copy away from faces and garment identity markers.
- Do not cover a real garment logo, print, embroidery, collar, closure, pockets, waist construction, or hem.
- Base copy only on the visible scene, styling mood, locked garment facts, or confirmed composition.
- Adult scene-oriented examples include `海边漫步`, `城市街拍`, `花园漫游`, `户外旅行`, `森林漫步`, and `休闲咖啡`.
- Child scene-oriented examples include `乐园时光`, `校园漫步`, `课间活力`, `公园探索`, `快乐阅读`, and `童趣日常`. Never use adult-coded child copy such as `休闲咖啡`, `通勤日常`, `商务休闲`, or `都市约会`.
- Do not claim unsupported warmth, cooling, slimming, sun protection, waterproofing, breathability, elasticity, fiber content, or other functions.

## Props And Accessories

- Treat accessories and props in the approved references as mood examples only.
- Do not add bags, hats, sunglasses, jewelry, scarves, belts, backpacks, outer layers, or handheld props unless source-supported or explicitly approved.
- Even when approved, reject any prop or accessory that alters, covers, or changes perception of the garment.

## Prompt Block

Include this information in `four_grid_plan` before generation:

- Panel 1: unique model identity, pose, standing/seated status, companion garments, footwear/legwear, scene use case, scene, framing, exact Chinese title/subcopy.
- Panel 2: unique model identity, pose, standing/seated status, companion garments, footwear/legwear, scene use case, scene, framing, exact Chinese title/subcopy.
- Panel 3: unique model identity, pose, standing/seated status, companion garments, footwear/legwear, scene use case, scene, framing, exact Chinese title/subcopy.
- Panel 4: unique model identity, pose, standing/seated status, companion garments, footwear/legwear, scene use case, scene, framing, exact Chinese title/subcopy.
- Central copy: mandatory exact headline and mandatory exact subline. `none` is forbidden.
- Cross-panel locks: four distinct white European/Western faces, no Black or other non-white model, four distinct poses, four distinct outfits, exactly 3 standing and 1 seated, same exact SKU in all panels, no garment obstruction.
- Copy-layout lock: exactly five copy blocks total; one centered main block at the panel crossing and one copy block inside each panel; consistent panel-copy alignment and spacing; no missing, extra, merged, duplicated, or floating text blocks.

The seated panel may occupy any quadrant, but the prompt must identify it explicitly. Vary panel order across SKUs when useful.

## Verification

Reject and regenerate if any condition is true:

- The result is not a true four-panel composition.
- Any face is repeated or near-duplicated.
- Any model is Black or otherwise not visibly white European/Western.
- Any pose is repeated or differs only by mirroring, camera angle, or minor limb movement.
- Any outfit repeats the same companion apparel combination or differs only by color, hairstyle, camera angle, pose, or a styling detail that is not clearly visible.
- The standing/seated count is not exactly 3:1.
- Any panel uses the wrong model age or gender context.
- Any child panel uses a cafe, coffee shop, bar, business/commuting setting, luxury lobby, nightlife, dating, or other adult social scene; or a childrenswear collage uses fewer than three preferred child-scene categories from [scene-context.md](scene-context.md).
- Any panel changes or hides a locked garment fact.
- Any face is cropped, blurred, turned fully away, or covered.
- Chinese copy is garbled, misspelled, excessive, unsupported, or placed over a face or garment identity marker.
- The output does not contain exactly five copy blocks.
- The central headline/subline block is missing, off-center, merged into a panel block, or not visually distinct.
- Any panel lacks its own title/subline block, contains more than one copy block, or uses placement inconsistent with the other panels.
- Props or accessories introduce unsupported styling or obstruct garment verification.
- Layout, dividers, or title bands make a panel too small to verify the SKU.
