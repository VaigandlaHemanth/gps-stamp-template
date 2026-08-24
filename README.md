# GPS Stamp Template

A browser tool that overlays a GPS-camera style location stamp onto a photo. Everything
runs locally in the page — the photo never leaves your device.

**Live:** https://vaigandlahemanth.github.io/gps-stamp-template/

## What it does

Drop in a photo, type the place name, address, coordinates, date and time, and it draws
the stamp panel over the bottom of the image. Download as JPG or PNG at the photo's
full resolution.

The layout was reverse-engineered from reference photos rather than eyeballed. Fitted at
1200px wide by maximising pixel overlap against the originals:

| Element | Value |
| --- | --- |
| Panel | inset 16px, 12px from the bottom, corner radius 36 |
| Tint | black at 50% |
| Map thumbnail | 290×290, vertically centred, 28px in |
| Text origin | x = 354 from panel left, wrap width 778 |
| Title | Inter SemiBold 65.4px, +0.75 tracking, 103 line pitch |
| Body | Inter Regular 55.2px, 76.5 line pitch |

Every value is a fraction of the image width, so it scales to any resolution. Text lands
within ±1px of the reference on all three test photos.

The typeface is **Inter**, not Roboto — that was settled by rendering candidates over the
original pixels and comparing overlap, where Inter scored 0.80–0.87 IoU and Roboto needed
a different letter-spacing on every line.

## Map thumbnail

Three sources:

- **Real tiles** — Voyager, Esri, Positron or OpenStreetMap, fetched for the coordinates
  you type. Works with no setup.
- **Google Maps** — needs your own Maps Static API key (see below). The only source that
  returns genuine Google cartography.
- **Your own screenshot** — drag, click, or Ctrl+V an image of the map.

### Using a Google Maps key

1. console.cloud.google.com → create a project
2. APIs & Services → Library → enable **Maps Static API**
3. APIs & Services → Credentials → create an API key
4. Restrict it: **Application restrictions → Websites** → add
   `https://vaigandlahemanth.github.io/*`, and **API restrictions → Maps Static API** only
5. Paste it into the tool's key box — it's saved in that browser's local storage

The key is never committed to this repo. Restricting by referrer is the real protection,
since any browser key is visible in its own network requests.

## Sizing

Four controls, all at 100% = the exact original:

- **Stamp size** — scales panel, text and map together
- **Text size** — lettering only; the panel grows taller to fit
- **Box width / height** — reshape just the panel

Or drag the handles on the preview: corners scale the whole stamp, the right edge sets
width, the top edge sets height. Works with mouse, finger or pen.

**⛶ Full screen edit** enlarges the preview and moves the sliders underneath it, for
phones.

## Notes

- Needs internet on first load to fetch Inter from Google Fonts. If it can't, the page
  says so rather than silently substituting a different font.
- Body text size is a compromise: letter-only lines fit 54.2px and digit-heavy lines
  56.2px, so it uses 55.2px, keeping every line within ~2% of the original width.
- The datetime line ends in a stray comma by design — the reference app clips its
  timezone. There's a dropdown to show it instead.

## Licence

MIT.
