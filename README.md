# xiuyuan0216.github.io

Source for Xiu Yuan's academic website: https://xiuyuan0216.github.io/

## Structure

- `index.html` — the whole site, one semantic page (hero, research, experience, education, publications)
- `stylesheet.css` — design tokens, layout, and components; light + dark themes
- `images/` — original assets
- `images/media/` — web-optimized derivatives actually referenced by the page
  (MP4 + poster frames instead of multi-megabyte GIFs, resized logos and figures)

## Editing

Publications are plain `<article class="pub">` blocks in `index.html`. Copy one,
swap the media, title, authors, venues, links, and abstract. Add
`pub--featured` to the `<article>` to highlight a representative paper.

## Regenerating optimized media

```bash
# animated media -> mp4 + poster
ffmpeg -i images/SOURCE.gif -movflags +faststart -pix_fmt yuv420p -an \
  -vf "scale='min(720,iw)':-2:flags=lanczos,fps=15" -c:v libx264 -crf 30 -preset slow \
  images/media/NAME.mp4
ffmpeg -i images/SOURCE.gif -vframes 1 -vf "scale='min(720,iw)':-2" -q:v 6 images/media/NAME.jpg
```

Adapted from [Jon Barron](https://jonbarron.info/)'s academic website template.
