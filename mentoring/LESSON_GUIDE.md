# Reusing the lesson shell for new materials

The mentoring deck is now driven entirely from the `lessonLibrary` object defined near the bottom of `mentoring.html`. Each top-level key inside `lessonLibrary` becomes a selectable template in the "Lesson template" dropdown, and the associated data is what renders the slides, slide map, and saved notes.

## 1. Add a new lesson entry
1. Open `mentoring/mentoring.html` and locate the `lessonLibrary` constant (search for `const lessonLibrary = {`).
2. Duplicate one of the existing lesson objects (e.g., `mentoringOrientation` or `eltLessonTemplate`) and give it a new key. The key is what the selector uses internally.
3. Update the `id`, `label`, and `meta` fields:
   - `id` should be unique; it is also used to namespace saved slide notes in `localStorage`.
   - `label` is what appears in the dropdown.
   - `meta` is optional but lets you customise the eyebrow text, descriptive line under the title, and the browser page title.【F:mentoring/mentoring.html†L1209-L1268】【F:mentoring/mentoring.html†L1739-L1767】

## 2. Define slide map sections (optional but recommended)
Set the `sections` array to control the headings that appear in the slide map. Each section needs a `title` and the `slideKeys` that belong to it. The keys must match the `key` property for each slide configuration you define later.【F:mentoring/mentoring.html†L1218-L1234】

## 3. Supply the slide configurations
Add objects to the `slides` array in the order you want them to appear. Every slide object needs at least a unique `key` and a `type`. Supported slide types and their fields are:

### `hero`
Use for the opening slide. Accepts `title`, `subtitle`, and an `image` object with `src` and `alt`. The optional `nav.hidePrev`, `nav.nextLabel`, and `nav.nextIcon` fields customise the navigation buttons.【F:mentoring/mentoring.html†L1235-L1252】【F:mentoring/mentoring.html†L3102-L3131】

### `content`
Displays rich text with optional media and lists. Fields include `icon`, `title`, `subtitle`, `image`, `body` (array of paragraphs), and `list`. Lists can be a simple array of strings or an array of objects with `letter`/`text` pairs when you set `listStyle` (e.g., SMART goals).【F:mentoring/mentoring.html†L1253-L1397】【F:mentoring/mentoring.html†L2800-L2827】

### `cards`
Shows multiple callouts side by side. Provide `cards`, an array of objects with optional `icon`, `title`, and `description` values.【F:mentoring/mentoring.html†L1362-L1379】【F:mentoring/mentoring.html†L2829-L2856】

### `story`
Combines a quote, imagery, and short narrative paragraphs. The optional `process` and `outcome` objects display bold labels followed by explanatory text.【F:mentoring/mentoring.html†L1370-L1388】【F:mentoring/mentoring.html†L2858-L2896】

### `process`
Ideal for flows or procedures. Supply `steps`, an array where each item can include `title`, `description`, and `duration`. Any `image` or `body` content you add will render above the stepper.【F:mentoring/mentoring.html†L1398-L1427】【F:mentoring/mentoring.html†L2898-L2953】

### `quiz`
Renders single-answer checks for understanding. Each question needs an `id`, `prompt`, `options` (array of `{ value, label }`), an `answer`, plus feedback strings. The button wiring is automatic.【F:mentoring/mentoring.html†L1428-L1458】【F:mentoring/mentoring.html†L2955-L3023】

### `reflection`
Creates textarea fields for planning notes or reflections. Pass a `fields` array where each entry can define `id`, `label`, and `placeholder`. Navigation defaults to a "Finish & Restart" button on the last slide, but you can override it via the slide's `nav` object.【F:mentoring/mentoring.html†L1677-L1695】【F:mentoring/mentoring.html†L3025-L3073】

If you omit a `type`, the slide falls back to the `content` renderer.

## 4. Load your lesson in the browser
Once your lesson object is defined:
1. Open `mentoring/mentoring.html` in a browser.
2. Use the "Lesson template" dropdown at the top of the page to switch to your new template. The slides, slide map, and notes panel will regenerate instantly with your data.【F:mentoring/mentoring.html†L1160-L1168】【F:mentoring/mentoring.html†L3146-L3204】

Because notes are stored per lesson `id`, switching templates will keep your annotations separate for each lesson. You can export and import notes from the toolbar as before.【F:mentoring/mentoring.html†L2549-L2569】

## 5. Reusing assets
Images are linked by URL. If you need local assets, host them in the repository (e.g., under `mentoring/assets`) and point the `image.src` to the relative path. Make sure every image has meaningful alt text for accessibility.

With these steps, you can duplicate the mentoring deck structure for any other instructional purpose—ELT lessons, professional learning sessions, or completely different subjects—without editing the rendering logic.
