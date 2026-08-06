---
name: garment-product-image-guard
description: Preserve original garment facts in clothing ecommerce images using mandatory source references, SKU_PROFILE.json identity locks, prompt-lock injection, age-appropriate scenes, and strict wrong-style rejection. Use for SKU batches, white-background views, face-visible model views, four-grid lifestyle collages, generated detail cards, fixed-layout fabric cards, or any task that must match source clothing without color, pattern, cut, material, logo, accessory, or construction drift. For childrenswear, prioritize amusement parks, school campuses, playgrounds, parks, libraries, and children's activity spaces; reject cafes and adult social, business, commuting, nightlife, or dating settings.
---

# Garment Product Image Guard

Use this skill to generate or review apparel ecommerce imagery with strict fidelity to the original SKU photos. Prioritize stability and source consistency over speed, beauty, variation, or creative interpretation.

## Highest-Priority Generation Contract

The image-generation prompt is the execution contract. Do not rely on this skill text, a short user request, or post-generation review to preserve garment identity. Before every image-generation call, compile a `PROMPT_LOCK_BLOCK` from the current `SKU_PROFILE.json` and source images, then paste it into the image-generation prompt.

Every final image prompt must include:

- The exact source image filenames used as evidence for the requested view.
- The requested output filename and view, such as `SKU_01_front_white.jpg`.
- Verbatim or lossless text from `identity_lock`, including category, silhouette/length, front markers, back markers, sleeve markers, color/material, evidence filenames, and negative constraints.
- Verbatim or lossless text from `print_lock`, `source_role_map`, `view_specific_details`, `closure_lock`, `pocket_lock`, `belt_lock`, `sleeve_lock`, `collar_lock`, and `hem_lock`.
- The complete `scene_context_lock` for every model-worn or four-grid output, including model age group, preferred/allowed/forbidden scene categories, scene rationale, and age-appropriate copy direction. Follow [references/scene-context.md](references/scene-context.md).
- The matching `detail_source_map` entry and accepted flat-lay rendering base for detail outputs. For fabric outputs, include the complete fixed `fabric_layout_plan`, composition status/evidence, source-supported characteristics, accepted garment-thumbnail base, and macro evidence.
- The complete `four_grid_plan` for four-grid outputs, including four distinct white European/Western model identities, four distinct poses, four visibly different companion-apparel styling plans, exactly three standing poses and one seated pose, panel scenes, and the mandatory five-block Chinese copy layout: one central headline/subline block plus one title/subline block inside each of the four panels. Treat the source SKU as the unchanged hero product and vary the secondary garments worn with it to demonstrate scene versatility.
- Explicit negative constraints that block likely drift for this SKU and view.
- The sentence: `This is exact SKU replication, not creative fashion generation. Zero deviation from source garment facts.`

If any high-risk lock is missing, generic, or not view-specific enough, stop before generation, inspect the source images again, update `SKU_PROFILE.json`, and only then generate. A prompt that says only "keep the original style" or "match the source image" is not sufficient.

## Source Image Reference Rule

Always use source images as active references, not just as background context.

- When the image tool supports attached or referenced source images, attach the original SKU source images with the strongest available fidelity/reference strength. Text-only prompting is insufficient when image reference is available.
- With built-in image generation over local files, inspect the exact source images or source contact sheet with `view_image` immediately before prompting so the source garment is visible in the conversation context.
- For view-specific outputs, include the source images that prove that view or detail. For detail outputs, use the accepted AI-generated `SKU_01_front_white.jpg` or `SKU_02_back_white.jpg` as the primary rendering reference and the original source photos only as secondary garment-fact evidence. Use a tag image for fabric composition.
- Never use an original hanger, wall, clip, mannequin, worn, wrinkled, or casual real-photo view as the visual base of a final detail card.
- If the backend cannot attach image references, record that downgrade in the batch log and compensate by using the full `PROMPT_LOCK_BLOCK`. Do not treat text-only generation as equivalent to referenced generation.

## Required Prompt Template

Use this template for every image-generation prompt. Fill it from `SKU_PROFILE.json`; do not invent missing facts.

```text
EXACT SKU REPLICATION TASK
Output file: <required filename>
Requested view/type: <front white | back white | model front | model back | four-grid lifestyle collage | detail A | detail B | fabric>
Source images to use as binding visual references: <filenames and source roles>

PROMPT_LOCK_BLOCK - paste from SKU_PROFILE without weakening:
identity_lock.category_and_subcategory: <text>
identity_lock.overall_silhouette_and_length: <text>
identity_lock.front_identity_markers: <text>
identity_lock.back_identity_markers: <text>
identity_lock.sleeve_identity_markers: <text>
identity_lock.color_and_material_appearance: <text>
identity_lock.negative_constraints: <list>
print_lock: <text/list>
source_role_map: <relevant entries>
view_specific_details: <front/back/side-only facts>
closure_lock: <text>
pocket_lock: <text>
belt_lock: <text>
sleeve_lock: <text>
collar_lock: <text>
hem_lock: <text>
scene_context_lock: <required for model and four-grid outputs; include age group, preferred/allowed/forbidden scenes, rationale, and copy direction>
detail_source_map for this output: <only when detail/fabric>
four_grid_plan: <only when four-grid; include panel-by-panel model identity, pose, standing/seated status, companion_garments, footwear_or_legwear, scene_use_case, scene, framing, and exact Chinese copy>
accepted flat-lay rendering base: <SKU_01_front_white.jpg or SKU_02_back_white.jpg; required for detail outputs>
composition evidence: <only when fabric>
fabric_layout_plan: <only when fabric; include fixed left/right split, exact left-column order/copy, composition block or omitted, source-supported characteristics, thumbnail base, and macro evidence>

Output styling:
<white-background rules OR model-scene rules OR four-grid layout rules OR detail/fabric layout rules>

Drift blockers:
Do not simplify, beautify, normalize, symmetrize, replace, reinterpret, relocate, mirror, add, or remove garment construction.
Do not change color, pattern, print/logo, collar, sleeve, placket, pockets, belt/tie/buckle, hem, seams, length, fabric behavior, or view-specific details.
This is exact SKU replication, not creative fashion generation. Zero deviation from source garment facts.
```

Reject the prompt before generation if this template is not filled with concrete SKU facts.

## Common Drift Blockers

Add these blockers to the prompt when the matching risk exists:

- Collar/neckline: `Do not change the collar/neckline type, edge trim, placket relationship, lace/stand/round/V geometry, or move a back-neck feature to the front.`
- Sleeves: `Do not change sleeve length, volume, cuff/opening, transparency, shoulder gathers, or lace/sheer behavior; do not convert straight sleeves into puff, bishop, balloon, lantern, ruffled, or gathered sleeves.`
- Belts/ties: `Do not change belt/tie type, buckle shape, buckle scale/material, knot/bow shape, holes, tail direction, loop placement, side/center position, or waist construction. Do not turn side ties into a center-front bow/belt.`
- Pockets: `Do not change pocket count, side, angle, opening shape, flap/welt/patch/cargo type, button placement, seam relation, or front/back placement.`
- Hem/length: `Do not normalize an asymmetric, one-side slanted, high-low, curved, scalloped, or irregular hem into a symmetric level hem. Do not make a symmetric hem asymmetric.`
- Print/pattern/logo: `Do not simplify, resize, recolor, rotate, mirror, move, omit, or invent any print, logo, embroidery, stripe, check, floral repeat, or color block.`
- Fabric: `Do not change transparency, sheen, weave/knit, thickness, drape, wrinkle behavior, lining visibility, or confirmed composition.`
- Child scene: `Keep the setting clearly age-appropriate. Prefer amusement park, school campus, playground, park, library, or children's activity settings. Do not place a child model in a cafe, bar, business lounge, office, commuting, luxury-lobby, nightlife, dating, or other adult social scene.`

## Non-Negotiables

Treat the source image set and `SKU_PROFILE.json` as binding truth.

Never:

- Change color.
- Change style, category, version, or silhouette.
- Change pattern, print, embroidery, graphic placement, or logo placement.
- Invent details that are not visible or recorded.
- Add a logo.
- Add accessories or props that cover or visually alter the garment.
- Change cut, tailoring, garment length, sleeve shape, collar shape, placket, zipper, buttons, pockets, hem, seams, or key construction.
- Change material texture, weave, knit, sheen, thickness, transparency, drape, or fabric behavior.
- Deliver an output inconsistent with the original garment.

If a requested edit conflicts with these rules, keep the garment facts unchanged and explain that the request would break SKU fidelity. Preserve real garment logos/prints that exist in the source; remove only external watermarks, unrelated overlay logos, hangers, security tags, clutter, and background interference.

## Workflow

1. Scan the input folder once and build the SKU queue before generating anything.
2. Treat one root-level image as one SKU, or one subfolder as one SKU containing all images for that product.
3. Never mix materials across folders or SKUs.
4. Skip hidden, corrupt, non-image, and already completed SKUs.
5. For each SKU, create or read `SKU_PROFILE.json` before generating final images.
6. Build the SKU identity lock and confirm it is specific enough to distinguish this exact garment from similar items.
7. Generate `SKU_01_front_white.jpg` first for new or invalid SKUs, using the required prompt template and source references.
8. Verify `SKU_01_front_white.jpg` against the source images and locks before generating any other output. If it fails, update the locks and retry before continuing.
9. Before planning any model or four-grid output, read [references/scene-context.md](references/scene-context.md), classify the model age group, and write `scene_context_lock`; never use an adult-default scene for childrenswear. Generate detail outputs only after the matching front/back white image passes verification; use that accepted flat-lay image as the primary rendering reference and original photos only to verify facts. Generate all other remaining outputs from the profile, accepted evidence, and required prompt template, not from memory or free guessing.
10. Generate `SKU_05_four_grid.jpg` as one fresh generative-AI image after the front white image and model direction pass verification; never locally assemble it. Verify each panel against the SKU locks, then verify cross-panel model, pose, layout, and copy requirements.
11. Verify that every required output is a generative AI output, not locally derived pixel processing.
12. Verify every output against the profile and SKU identity lock before accepting it.
13. Retry a failed or inconsistent image up to 2 times, log failures, and continue the batch.
14. When the user reports a wrong garment fact, immediately re-check the source images, update `SKU_PROFILE.json` with a concrete correction lock before any regeneration, mark existing failed outputs as `INVALID`, and use the correction lock in all retry prompts.

Before generating model, detail, or fabric outputs, treat the user's approved ecommerce examples as the visual standard: model images use cinematic/poster-like real-life scenes with visible faces, premium texture, natural light, and editorial composition; detail images use polished ecommerce copy layouts; fabric images use the mandatory layout in [references/fabric-layout.md](references/fabric-layout.md); composition text is used only after it is confirmed from input evidence. Reference examples define image mood and quality only, never garment facts.

Before marking composition as unknown, inspect every source image that may contain a hang tag, certificate, neck label, wash label, fabric label, barcode tag, or care instruction card. Zoom, crop, rotate, or build local reading aids only for fact extraction and verification. If readable text includes `成分`, `面料`, `材质`, `含量`, `composition`, `material`, `fabric`, `content`, or a fiber percentage, record the exact composition in `SKU_PROFILE.json` with the source filename as evidence. Do not mark composition unknown when a readable tag or label in the SKU source images states it.

Use generative AI image generation for image creation. If files are saved locally, describe them as "generated by AI and saved to the local workspace", not as locally synthesized images.

## Generative AI Requirement

Every new final product image and every regeneration attempt must be created by an actual generative-AI image tool call. This is mandatory, including white-background, model, detail, fabric, and any replacement output.

Never use a local image-generation workflow as a substitute. Do not invoke local diffusion/checkpoint models, image-to-image pipelines, scripted renderers, template engines, screenshots, or any other local process to generate a final product image. If a generative-AI image tool is unavailable, stop the image-generation step, record the blocker, and ask for access or direction; do not produce a local fallback.

Saving an AI-generated result to the local workspace is allowed. The local workspace is storage only, not an image-generation backend.

Local scripts or image-processing libraries may be used only for:

- Scanning input folders and output folders.
- Reading metadata, dimensions, and file integrity.
- Creating or updating `SKU_PROFILE.json`.
- Renaming, moving, or converting an already AI-generated image without changing visual content.
- Building contact sheets, previews, and verification aids.
- Writing batch logs.

Local scripts or image-processing libraries must never be used to create a required final product image by cropping, compositing, retouching, drawing text, changing backgrounds, making fabric cards, detail cards, model mockups, or otherwise synthesizing the final visual. A locally derived image is not acceptable as a required output, even when it preserves SKU facts.

Do not generate one AI contact sheet, poster, or collage and crop it into the required final outputs. Each required output file must be accepted as its own AI-generated ecommerce image, or as a previously verified AI output reused without visual modification.

For every required output, record generation provenance in the batch log, including the generative-AI tool used and the generation timestamp:

- `AI_GENERATED`: generated by an actual generative-AI tool call from the SKU source images and `SKU_PROFILE.json`.
- `AI_REUSED`: reused from a previous verified generative AI output without visual modification.
- `INVALID_LOCAL_DERIVED`: created by local pixel processing and must be regenerated with generative AI.

A SKU is complete only when every file listed in `required_outputs` is either `AI_GENERATED` or verified `AI_REUSED`, `SKU_PROFILE.json` exists, and all outputs pass the verification gate.

## SKU Identity Lock

Prevent wrong-style and wrong-SKU outputs before optimizing beauty or scene variety.

Before generating any final image, create an `identity_lock` entry in `SKU_PROFILE.json`. The lock must be concrete enough that another similar garment would fail it.

Record:

- Exact garment category and subcategory, such as T-shirt vs polo, cardigan vs pullover, shirt dress vs blouse, jeans vs tailored trousers.
- Overall silhouette and length, including shoulder shape, body width, waist shape, hem length, and front/back proportion.
- Front identity markers: neckline, collar, placket, buttons, zipper, pocket count and placement, print/logo/pattern placement, hem shape, and any asymmetric details.
- Back identity markers: back neckline, yoke, seams, darts, zipper, buttons, keyhole, belt, pocket, print/logo/pattern, and hem shape.
- Sleeve identity markers: sleeve length, cuff shape, sleeve opening, shoulder seam, drop shoulder, raglan, gathers, pleats, or trim.
- Color and material appearance: exact visible color family, contrast colors, knit/weave, sheen, thickness, transparency, drape, and wrinkle behavior.
- Negative constraints: visually similar garments that must not be generated, such as "not a polo collar", "not a hoodie", "not a blazer", "not a pleated skirt", "not generic slash pockets", or "not a plain item without the print".
- Evidence filenames for each high-risk identity marker.

Before each generation, compile and paste the required `PROMPT_LOCK_BLOCK` from `identity_lock`, `print_lock`, `source_role_map`, `view_specific_details`, `closure_lock`, `pocket_lock`, `belt_lock`, `sleeve_lock`, `collar_lock`, `hem_lock`, and the relevant `detail_source_map`. The prompt must say the output is the same SKU, not a similar garment, and must include concrete positive facts, exact evidence filenames, and negative constraints. Do not summarize away high-risk construction details.

If the source images are insufficient to lock a high-risk view, mark that field `LOW_CONFIDENCE_VIEW` and generate only conservative facts visible or strongly implied by the source. Do not invent a nicer, more common, more complete, or trendier garment to fill gaps.

Reject and regenerate if:

- The output changes the garment into a different subcategory or retail style.
- The output preserves color but changes construction, collar, closure, pockets, print, sleeve, hem, or silhouette enough to look like a different product.
- The output looks like a generic catalog item inspired by the source instead of the exact SKU.
- The model-worn output changes the garment fit so much that key identity markers are no longer auditable.

## Cinematic Model Image Standard

Use the user's approved model examples as style references for `SKU_03_model.jpg` and `SKU_04_model_back.jpg`.

The reference style means:

- Cinematic/poster-like ecommerce image, not a flat studio catalog shot.
- Premium outdoor or real-life editorial scene selected from [references/scene-context.md](references/scene-context.md) for the model's age group. For children, prioritize amusement park, school campus, playground, park, library, or children's activity spaces; never use a cafe or adult social/business setting.
- Natural directional light, soft shadows, subtle cinematic color grading, shallow background depth, realistic skin and fabric texture, and high-resolution fashion photography quality.
- Confident natural pose, visible face, clean styling, and enough environment to feel like a campaign poster.
- Front and back model images should feel like a matched editorial pair for the same SKU, with compatible model, scene mood, lighting, and color grade.

The reference style does not mean:

- Do not copy the reference garment category, trench details, sage color, buttons, belt, pants, sea background, or styling unless those facts are present in the source SKU.
- Do not add wind, motion, dramatic pose, open-front styling, tucked fabric, rolled sleeves, extra layering, or accessories if they hide or change SKU identity markers.
- Do not prioritize atmosphere over garment verification. The garment must remain the same SKU first, and cinematic second.

For model prompts, include both:

- Style direction: cinematic poster feel, premium editorial lifestyle scene, natural light, shallow depth, high texture, visible face.
- SKU lock direction: preserve exact source garment category, silhouette, collar/neckline, closure, pocket geometry, hem, sleeve shape, print/logo/pattern, color, and fabric behavior.

Reject and regenerate if:

- The model image looks flat, low-end, over-smoothed, plastic, generic catalog, or lacks cinematic/poster quality.
- The scene, pose, wind, crop, lighting, or styling hides any key identity marker needed to verify the exact SKU.
- The image borrows garment details from the style reference or invents a more cinematic but wrong garment.

## Print, Text, Logo, And Pattern Lock

For any garment with visible print, text, embroidery, logo, patch, allover pattern, stripe, color block, or graphic artwork, create a `print_lock` entry in `SKU_PROFILE.json` before generating images.

The `print_lock` must record:

- Exact visible text or approximate text when partially unreadable.
- Text order from top to bottom and left to right.
- Graphic shapes, icons, symbols, patches, badges, and illustration elements.
- Main colors and outline colors.
- Placement on the garment, such as center chest, left chest, hem, sleeve, back, collar, pocket, or allover repeat.
- Relative size, spacing, rotation, and alignment.
- Which source image is the primary evidence.
- `LOW_CONFIDENCE_TEXT` for any unreadable text.

During generation, the prompt must explicitly state that the garment print is an identity-locked product detail, not decorative inspiration. The generated result must copy the original print/pattern/logo layout and placement. If exact text reproduction is unlikely, prefer a closer flat-lay or detail output over an invented or simplified graphic.

Reject and regenerate if:

- Any visible text changes, disappears, becomes a different word, or appears in the wrong order.
- A graphic is simplified, replaced, mirrored, rotated incorrectly, resized materially, or moved.
- A logo, patch, embroidery, motif, stripe, or color block is added, removed, or changed.
- A repeated pattern changes density, motif shape, color, direction, or spacing.
- A model pose, fold, shadow, or copy text hides the garment print needed to verify identity.

## View, Detail, And Geometry Locks

Before generating or accepting any output, bind visible construction details to their source image role. Do not let the model reinterpret a back detail as a front detail, a front detail as a back detail, or a side-specific detail as symmetric.

Record these locks in `SKU_PROFILE.json` when visible:

- `source_role_map`: classify each source image as `front`, `back`, `side`, `inside_label`, `tag`, `neck_front`, `neck_back`, `waist_front`, `waist_back`, `pocket_detail`, `fabric_detail`, or `unknown`.
- `view_specific_details`: list front-only, back-only, left-side-only, right-side-only, and unknown-side details with evidence filenames.
- `closure_lock`: record fastening location and side, such as front placket, back neck keyhole, rear button loop, side zipper, fly front, button count, button position, and whether the closure is visible.
- `pocket_lock`: record pocket count, garment side, opening shape, opening angle, depth, relation to waistband, relation to pleats or seams, and whether the pocket is curved, slanted, welt, flap, patch, cargo, or hidden.
- `belt_lock`: classify the waist item as fabric self-tie, sash, fixed side tie, removable belt, covered buckle belt, exposed metal/plastic buckle, D-ring/loop, waist tab, or no belt. Record buckle shape/material/size, covered or uncovered buckle, belt holes, knot/bow shape, tie location, belt tail direction and length, crossing or overlap, belt loop count and placement, and any asymmetry.
- `sleeve_lock`: record sleeve length, volume, seam/drop shape, transparency, cuff/opening shape, and whether the sleeve is straight/slim, puff, bishop, balloon, gathered, flared, ruffled, or layered.
- `collar_lock`: record collar/neckline geometry, such as stand collar, round neck, lapel, sailor/V yoke, lace collar, shirt collar, rib trim, placket relationship, and front/back collar differences.
- `hem_lock`: record whether the hem is straight, scalloped, curved, high-low, one-side slanted, irregular, asymmetric, or intentionally uneven. Record the long side, short side, slope direction, and evidence filename when visible.
- `detail_source_map`: for each planned detail image, record the detail name, original evidence filename and role, exact construction facts, matching accepted flat-lay rendering base (`SKU_01_front_white.jpg` or `SKU_02_back_white.jpg`), and the intended clean ecommerce composition.
- `scene_context_lock`: for model-worn and four-grid outputs, record the model age group, preferred scenes, allowed scenes, forbidden scenes, selected-scene rationale, and age-appropriate copy direction from [references/scene-context.md](references/scene-context.md).

Generation prompts must state these locks explicitly. For example, a closure seen only on a back-neck source image is a back-neck closure and must never become a front neckline feature. Trousers with a curved front pocket opening must not be normalized into generic diagonal slash pockets.

Reject and regenerate if:

- A front-only, back-only, or side-specific feature appears on the wrong view.
- A rear button, rear keyhole, back neck loop, back zipper, or back placket is moved to the front.
- A front closure, fly, placket, button, pocket, belt tail, belt hole, or buckle detail is moved, mirrored, simplified, or made symmetric when the source is asymmetric.
- Pocket shape, angle, depth, side, seam relation, or waistband relation changes.
- Belt type changes, such as fabric tie becoming a buckle belt, buckle belt becoming a bow/sash, fixed side tie becoming a center-front belt, or no-belt garments gaining a belt.
- Belt buckle shape, buckle scale, buckle material, belt holes, knot/bow shape, tie position, belt tail direction, crossing, overlap, loop placement, or waist construction changes.
- Sleeve volume, cuff/opening shape, transparency, lace/sheer behavior, or shoulder/gather construction changes.
- Collar/neckline type changes, such as stand collar becoming shirt collar, round neck becoming V neck, lace collar becoming plain collar, or back-neck detail moving to the front.
- Hem geometry changes, especially an asymmetric, one-side slanted, high-low, scalloped, or irregular hem becoming symmetric/level, or a symmetric hem becoming asymmetric.

## SKU Profile

Record these facts in `SKU_PROFILE.json`:

- Garment category.
- SKU identity lock with positive facts, negative constraints, and evidence filenames.
- Prompt-lock-ready fields that can be pasted directly into the required image-generation template.
- True color.
- Fit and silhouette.
- Collar or neckline.
- Sleeve type and length.
- Sleeve volume, cuff/opening, and shoulder/gather geometry when visible.
- Placket, zipper, button, and fastening structure.
- Pocket count, position, and shape.
- Source image role map.
- View-specific detail map for front-only, back-only, side-only, and unknown-side details.
- Closure geometry and location lock.
- Pocket geometry lock.
- Belt and waist construction lock when present.
- Collar/neckline construction lock when present.
- Hem geometry lock, including asymmetric or one-side slanted hems.
- Detail source map for each planned detail output.
- `four_grid_plan` with four panel entries. Record a unique model identity description, exact pose, `standing` or `seated`, visibly different companion garments, footwear/legwear, scene use case, framing, garment visibility requirements, and exact Chinese title/subcopy for each panel. Also record one mandatory exact central Chinese headline/subline. Require exactly five copy blocks, exactly three standing entries, one seated entry, and four different outfits built around the unchanged source SKU.
- View-specific negative constraints for likely drift, such as no collar substitution, no sleeve volume change, no belt/tie conversion, no pocket normalization, no hem symmetrizing, and no print/layout drift.
- Print, pattern, embroidery, and real garment logo facts.
- Fabric texture and material appearance.
- Front structure.
- Back structure.
- Key construction details.
- Composition, if read from tag, wash label, OCR, or trusted material data.
- Confidence flags such as `LOW_CONFIDENCE` when back view or composition is inferred.

Composition extraction rules:

- Treat readable source-tag composition as a locked product fact.
- Check both Chinese fields such as `成分`, `面料`, `材质`, `含量` and English fields such as `composition`, `material`, `fabric`, `content`.
- Accept exact values such as `面料：100%棉`, `成分：95.5%棉 4.5%氨纶`, or `100% cotton` only when visible in the SKU source image or reliable source material.
- Record the original wording when possible, plus a normalized display value for generation, for example original `面料：100%棉`, display `100%棉`.
- Add the evidence filename and confidence. Use `LOW_CONFIDENCE_COMPOSITION` only when the text is partially unreadable; do not use it when the tag is clear.
- If a hang tag and wash label conflict, prefer the clearer wash label for fiber content, record the conflict in `confidence_flags`, and do not invent a compromise.
- If a composition tag exists but is small, blurred, rotated, or partly blocked, create a local verification crop/contact sheet for reading. Local crops are allowed only for reading and logs, not as final product images.

Prefer source roles in this order:

- Color: front, then back, then detail.
- Front structure: front image.
- Back structure: back image.
- Neckline: matching-view neck detail, then matching-view full garment image.
- Zipper/placket/buttons: matching-view dedicated detail, then matching-view full garment image.
- Pockets: pocket detail, then matching front or back image; never infer a generic pocket shape.
- Belt and waist: waist detail, then front or back image matching the visible belt side.
- Fabric: fabric closeup, then body crop.
- Composition: tag/wash-label OCR, then material data, then unknown.

When real multi-image evidence exists, never override it with inference. If a single-image SKU lacks a back view, infer only conservative invisible-side facts and mark the profile as low confidence.

## Required Outputs

Generate 8 images per completed SKU:
- `SKU_01_front_white.jpg`: white-background front.
- `SKU_02_back_white.jpg`: white-background back.
- `SKU_03_model.jpg`: single-model front worn view.
- `SKU_04_model_back.jpg`: single-model back worn view.
- `SKU_05_four_grid.jpg`: square four-grid lifestyle collage with four distinct white European/Western models, four distinct poses, four distinct companion-apparel outfits built around the unchanged source SKU, exactly three standing poses and one seated pose, and exactly five restrained Chinese ecommerce copy blocks: one central block plus one block in each panel.
- `SKU_06_detail_A.jpg`: detail shot A.
- `SKU_07_detail_B.jpg`: detail shot B.
- `SKU_08_fabric.jpg`: fixed ecommerce fabric card with a left information column and dominant right-side near-distance fabric macro.

A SKU is complete only when all 8 outputs and `SKU_PROFILE.json` exist and pass consistency checks.
## Missing Output Detection

Before processing each SKU, inspect its output folder and compare existing files against the required output list.

Classify the SKU as:

- `COMPLETE`: all 8 required images and `SKU_PROFILE.json` exist and pass verification.
- `PROFILE_MISSING`: result images may exist, but `SKU_PROFILE.json` is missing.
- `PARTIAL`: `SKU_PROFILE.json` exists, but one or more required images are missing.
- `INVALID`: required files exist, but one or more outputs fail the verification gate.
- `PENDING`: no usable output folder exists.

For `PARTIAL` SKUs, generate only missing required images unless an existing image fails verification. Do not regenerate accepted existing outputs. For `INVALID` SKUs, regenerate only the failed image files. Log the exact missing or invalid filenames before generating.

Use this fixed expected filename set for every SKU:
- `SKU_01_front_white.jpg`
- `SKU_02_back_white.jpg`
- `SKU_03_model.jpg`
- `SKU_04_model_back.jpg`
- `SKU_05_four_grid.jpg`
- `SKU_06_detail_A.jpg`
- `SKU_07_detail_B.jpg`
- `SKU_08_fabric.jpg`
## Output Rules

White-background images:

- Use pure white background, centered product, natural light shadow, high resolution.
- Present the garment flattened, smooth, symmetric, and naturally spread.
- The garment must look fully laid flat and pressed, not hanging, floating, worn, curled, or casually placed.
- Hem lock: the bottom hem must preserve the source geometry and be fully visible from left side seam to right side seam. If the source hem is straight/symmetric, pull it flat and horizontally level; if the source hem is asymmetric, one-side slanted, high-low, scalloped, curved, or irregular, keep that exact visible geometry instead of normalizing it.
- Reject white-background outputs if the hem waves, curls upward, droops, folds under, hides the intended hem shape, changes a straight hem into a U/scallop, changes an asymmetric hem into a symmetric/level hem, changes a symmetric hem into an asymmetric hem, is hidden by shadow, or looks like a hanging-photo hem.
- Sleeves must be spread flat enough to show the real sleeve shape; preserve the source sleeve volume, cuff, transparency, and shoulder/gather construction. Reject curled, tucked, folded-under, twisted, puffed, bishop, balloon, ruffled, gathered, or slimmed sleeves unless that exact sleeve construction exists in the source.
- Collar must preserve the source neckline/collar geometry. Reject warped, collapsed, stretched, or substituted collars, including stand collar changed to shirt collar, round neck changed to V neck, lace collar changed to plain collar, or any back-neck detail moved to the front.
- Keep the real color, real pattern, real proportions, real fabric texture, and real garment logo/print.
- Remove hanger, security tag, watermark, unrelated overlay logo, clutter, and background noise.
- Reject outputs with warped collars, curled sleeves, distorted hems, hanging-photo posture, heavy wrinkles, asymmetric body shape, or any garment-fact drift.

Model images:

- Match model type to garment context: adult menswear, adult womenswear, or childrenswear.
- Use white European/Western models for every model-worn output while still matching the garment's adult/child and menswear/womenswear context.
- Reject any Black or other non-white model. Do not weaken this requirement through ambiguous terms such as `Western`, `international`, `diverse`, or `mixed`.
- Use cinematic/poster-like premium editorial styling with natural real-life scenes, directional light, shallow depth, high fabric texture, and a refined campaign feel.
- Keep the garment fully visible and unobstructed.
- Preserve the exact SKU identity on body: category, silhouette, collar/neckline, sleeve shape, closure, pocket geometry, hem, print/logo/pattern, and fabric behavior must remain auditable.
- The model's face must be visible in both `SKU_03_model.jpg` and `SKU_04_model_back.jpg`. For back-worn views, use a back or three-quarter-back pose with the head turned enough to show the face while still clearly showing the back of the garment.
- Model image backgrounds must not be pure white or white studio cutouts. Choose scenes through `scene_context_lock` and [references/scene-context.md](references/scene-context.md), then vary them across SKUs when possible. For childrenswear, prioritize amusement parks, school campuses, playgrounds, parks, libraries, or children's activity spaces; reject cafes, coffee shops, bars, business lounges, offices, commuting scenes, luxury lobbies, nightlife, dating, or other adult social settings even when they look visually premium.
- Do not add jewelry, bags, hats, scarves, belts, sunglasses, or props that alter perception of the garment unless such items are already in the source and required by the product.
- Reject model images if the face is cropped off, hidden, turned fully away, blurred beyond recognition, if the background is pure white, if the image lacks cinematic/poster quality, or if the cinematic styling causes wrong-style/wrong-SKU drift.

Four-grid lifestyle collages:
- Before planning or generating `SKU_05_four_grid.jpg`, read [references/four-grid.md](references/four-grid.md) completely and inspect all three bundled reference images named there.
- Generate one square 2-by-2 AI image with the exact same SKU in all panels, four different white European/Western faces, four different poses, four different outfits, exactly three standing and one seated, distinct lifestyle scenes, and exactly five restrained Simplified Chinese copy blocks: one central headline/subline block and one title/subline block inside every panel. Apply every SKU lock independently to all four panels; never locally assemble the output.
- Reject and regenerate for any violation listed in the four-grid reference, including repeated faces, poses, or outfits, wrong 3:1 standing/seated count, wrong garment facts, missing or extra copy blocks, a missing central copy block, any panel without its own copy block, inconsistent copy placement, garbled/unsupported copy, or obscured identity-critical details.
Detail shots:

- Choose real distinctive areas: neckline, placket, zipper, cuff, hem, pocket, print, shoulder seam, buttons, or special craft.
- Generate each detail card from the already accepted matching flat-lay output: use `SKU_01_front_white.jpg` for front details and `SKU_02_back_white.jpg` for back details. Keep the original source photos attached only as secondary evidence for construction, color, pattern, logo, and texture.
- Create a fresh generative-AI ecommerce close-up; do not crop, enlarge, mechanically reframe, or paste pixels from either the original real photo or the accepted flat-lay image.
- Keep the garment visibly flat, pressed, smooth, and naturally spread on a pure-white or very light neutral studio background. Preserve the clean flat-lay lighting and product geometry of the accepted white image.
- Compose the detail like the approved examples: one large, complete, sharply rendered construction area; generous clean negative space; restrained black/gray Chinese typography; a short title, thin divider, and one truthful subcopy line. Avoid heavy poster frames, busy icon grids, collage panels, or oversized headers that compete with the garment.
- Use macro clarity and include short Chinese ecommerce copy in every detail output. At minimum include a concise detail title such as `前领细节`, `后领细节`, `V领细节`, `圆领细节`, `印花细节`, `袖口细节`, `门襟细节`, `口袋细节`, or `下摆细节`, plus 1 short truthful subcopy line.
- Bind every detail shot to `detail_source_map` before generation. The prompt and review must name the original evidence filename and role, the accepted flat-lay rendering-base filename, and the exact visible construction facts.
- Use view-specific Chinese titles when the detail exists only on one view, such as `后领细节` for a back-neck button/keyhole. Use generic titles such as `领口细节` only when the same construction is visible and valid from the shown view.
- Keep detail copy away from the garment's identity-critical print, logo, embroidery, pattern, and construction details.
- Never feature details that do not exist on the source garment.
- If the chosen detail is not clearly visible in the accepted flat-lay image, regenerate and verify a better flat-lay image or choose another source-supported detail; never fall back to a crop of the original real photo.
- Reject detail shots that retain a hanger, clip, wall, outlet, security tag, mannequin, model, real-photo background, casual wrinkles, hanging posture, or photographic defects from the source; look like a source-photo crop; are plain macro photos without copy; use generic unrelated copy; hide the real detail; relocate it to the wrong view; or add non-source construction features.

Fabric image:

- Before planning or generating `SKU_08_fabric.jpg`, read [references/fabric-layout.md](references/fabric-layout.md) completely and inspect both bundled fabric-layout reference images.
- Treat the reference layout as mandatory, not optional: default 3:2 landscape; left 25-30% clean information column; right 70-75% one dominant near-distance fabric macro.
- Keep the fixed left-column order: `面料细节`, optional evidence-supported subtitle, confirmed `面料成分` block, 2-4 source-supported fabric characteristics, then one exact-SKU full-garment thumbnail at the bottom.
- Show composition only when exact fiber names and percentages are confirmed from readable same-SKU input evidence. When unconfirmed, omit the entire composition block and reflow the remaining content upward; never guess or show a placeholder.
- Use only source-supported characteristics. Do not infer comfort or performance claims from appearance.
- Preserve exact garment facts in the thumbnail and exact color, weave/knit, pattern scale, sheen, thickness, transparency, drape, and fold behavior in the macro.
- Reject and regenerate for any violation in the fabric-layout reference, including layout drift, wrong order, missing or wrong thumbnail, unsupported characteristics, guessed/placeholder composition, or generic/wrong fabric texture.

## Verification Gate

Before generating an image, verify the prompt itself. Reject and rewrite the prompt if it lacks source image filenames, the required `PROMPT_LOCK_BLOCK`, view-specific evidence, or concrete negative constraints. Do not call the image tool with a generic prompt.

Before accepting an image, compare it side by side against source images, `SKU_PROFILE.json`, the prompt used for generation, and the SKU identity lock. Use the strict standard: "same SKU", not "similar enough".

Perform this checklist for every output:

1. Confirm the prompt used the required template and contained concrete SKU facts, source filenames, and lock fields.
2. Match the overall product category, silhouette, length, front/back proportion, and intended wearing orientation.
3. Match all front, back, sleeve, collar/neckline, closure, pocket, hem, print/logo/pattern, and fabric identity markers.
4. Confirm every negative constraint from `identity_lock` and the prompt drift blockers is absent.
5. Confirm the output can be traced to evidence filenames in the SKU source set, not to assumptions from nearby SKUs or generic apparel knowledge.
6. Record pass/fail and the exact failed identity marker in the batch log.

Reject and regenerate if any answer is "yes":

- Did the prompt omit the required template, source image filenames, `PROMPT_LOCK_BLOCK`, or view-specific lock fields?
- Did the prompt rely on generic wording such as "keep original style" without concrete construction facts?
- Did the product become a different category, subcategory, retail style, or version?
- Did the output look like a similar catalog item rather than the exact SKU?
- Did the color drift?
- Did the print, pattern, embroidery, or real garment logo change?
- Did the cut, silhouette, collar, sleeves, hem, placket, zipper, buttons, pockets, or seams change?
- Did any front-only, back-only, or side-specific construction detail move to another view?
- Did a rear button, rear keyhole, rear loop, back zipper, or back placket become a front detail?
- Did a closure, button, fly, placket, zipper, belt, buckle, belt hole, belt tail, or waist detail move, mirror, disappear, or become generic?
- Did a fabric self-tie, side tie, sash, D-ring/loop, covered buckle, exposed buckle, waist tab, knot, bow, or belt tail change type, position, direction, scale, or side?
- Did a side waist tie become a center-front belt/bow/buckle, or did a center-front belt become a side tie?
- Did a pocket opening shape, angle, depth, side, seam relation, pleat relation, or waistband relation change?
- Did sleeve length, sleeve volume, cuff/opening shape, shoulder/gather structure, transparency, or lace/sheer behavior change?
- Did collar or neckline type, edge trim, placket relationship, lace collar, stand collar, or front/back collar geometry change?
- Did an asymmetric, one-side slanted, high-low, scalloped, curved, or irregular hem become symmetric/level, or did a symmetric hem become asymmetric?
- Did the fabric texture, sheen, weave, knit, thickness, drape, or transparency change?
- Did a model output lack cinematic/poster-like premium editorial quality?
- Did cinematic styling, wind, pose, crop, lighting, or scene choice hide or change SKU identity markers?
- Did a model output hide, crop off, blur, or turn away the model face?
- Did any model output use a Black or other non-white model instead of a white European/Western model?
- Did a model output use a pure-white or white studio background instead of a random lifestyle background?
- Did a model or four-grid prompt omit `scene_context_lock`, fail to classify the model age group, select a scene without an age-appropriateness rationale, place a child in a cafe, coffee shop, bar, business lounge, office, commuting, luxury-lobby, nightlife, dating, or other adult social setting, or give the child adult social/business copy?
- Did the model, pose, text, props, or scene obscure key garment details?
- Did a four-grid output violate any rule in [references/four-grid.md](references/four-grid.md), including four white European/Western models, panel count, unique faces, poses, and outfits, the 3:1 standing/seated count, same-SKU fidelity, exactly five readable Chinese copy blocks (one central and one per panel), consistent copy placement, and unobstructed garment facts?
- Did the image add details, accessories, decorative elements, logos, or trims not present in the source?
- Did a detail shot omit Chinese ecommerce copy, use copy unrelated to the actual source detail, or use a generic title that hides a front/back/side mismatch?
- Did a detail shot use an original real photo instead of an accepted front/back flat-lay output as its primary rendering base?
- Did a detail shot look cropped from a hanger, wall, clip, mannequin, model, or wrinkled real-photo view instead of freshly generated as a clean flat-lay ecommerce close-up?
- Did a fabric image violate [references/fabric-layout.md](references/fabric-layout.md), including the fixed left/right split, left-column order, evidence-only composition, source-supported characteristics, exact-SKU thumbnail, or exact right-side fabric macro?
- Does the output look like a similar garment instead of the same SKU?

Only deliver images that pass this gate.

## Batch Logging

Maintain the batch log at the output root unless the user specifies another path:

- Default path: `输出/batch_generation_log.md`
- If the workspace uses absolute clothing folders, use the output folder beside the SKU folders, for example `C:\Users\<user>\Documents\衣服\输出\batch_generation_log.md`.
- Append new runs to the log with a timestamp instead of overwriting prior run history.

Record:

- Total SKU count.
- Completed SKU count.
- Pending SKU count.
- Per-SKU missing output filenames.
- Per-SKU invalid output filenames.
- Failed image names and failure reasons.
- Per-output prompt-lock status, including whether source filenames and required lock fields were included before generation.
- Per-output identity lock pass/fail status and the exact failed marker for wrong-style outputs.
- Final unfinished SKU list.

Continue until the queue is empty unless the user explicitly asks to pause or stop.
