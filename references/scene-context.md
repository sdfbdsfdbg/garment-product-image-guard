# Age-Appropriate Scene Context

Read this file before planning, prompting, generating, or verifying any model-worn image or four-grid collage.

## Scene Context Lock

Create `scene_context_lock` in `SKU_PROFILE.json` with:

- `model_age_group`: `toddler`, `child`, `teen`, or `adult`; infer conservatively from the SKU category and source model evidence.
- `preferred_scenes`: age-appropriate scene categories to emphasize.
- `allowed_scenes`: acceptable alternatives.
- `forbidden_scenes`: settings and narratives that fail verification.
- `selected_scene_rationale`: one sentence explaining why the chosen scene is plausible for that age and garment.
- `copy_direction`: age-appropriate lifestyle language; never describe children with adult social, dating, commuting, or business narratives.

Include the complete lock in every model and four-grid prompt. If the age group is uncertain, select the younger conservative context and avoid adult-coded scenes.

## Childrenswear

Prioritize scenes that naturally support children's everyday life and movement:

- Amusement park, family theme park, carousel area, or colorful recreation park.
- School campus, school courtyard, playground, sports field, track, or safe school corridor.
- Public park, botanical garden, family picnic lawn, or child-friendly nature trail.
- Children's library, reading corner, art classroom, music room, science activity room, or children's museum.
- Indoor play center, family recreation space, dance studio, or supervised hobby/activity venue.

For a four-grid childrenswear collage, use at least three of the four panels from the preferred categories above. Keep all four settings distinct and plausible. A campus scene must read as a safe children's school environment, not an adult university or office campus.

Reject these scenes for child models:

- Cafe, coffee shop, tea room, restaurant social table, bar, pub, nightclub, or lounge.
- Office, coworking space, business lobby, commuting platform, business district, conference, or client-meeting setting.
- Luxury hotel lobby, adult boutique lounge, dating setting, nightlife street, or adult party/social scene.
- Any location, pose, styling, copy, or activity that makes the child look like an adult commuter, customer, professional, date, or nightlife participant.

Do not rescue an inappropriate scene merely by adding toys or bright colors. The location and activity themselves must be age-plausible.

Safe child copy examples include `乐园时光`, `校园漫步`, `课间活力`, `公园探索`, `快乐阅读`, and `童趣日常`. Avoid `咖啡小憩`, `通勤日常`, `商务休闲`, `都市约会`, `午后茶叙`, or similar adult-coded language.

## Teen And Adult Scenes

- For teens, prefer school campus, sports ground, library, park, shopping street, hobby studio, or daytime youth activity settings. Avoid bars, nightlife, dating-coded intimacy, and business-professional narratives unless the user explicitly supplies an appropriate adult model requirement.
- For adults, allow streets, architecture, courtyards, gardens, coast, cafe exterior/interior, commercial interiors, travel, and commuting scenes when they match the garment and do not obscure SKU facts.

## Verification

Reject and regenerate when:

- `scene_context_lock` is missing or the model age group is not stated.
- The setting conflicts with the model's apparent age or garment audience.
- A child appears in any forbidden adult-coded scene.
- Childrenswear four-grid scenes do not use at least three preferred child-scene categories.
- Scene copy describes an activity that is not visible, age-plausible, or supported by the setting.
- Props, furniture, signage, pose, or styling transform an otherwise neutral location into an adult social/business context.
