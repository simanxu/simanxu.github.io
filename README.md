# simanxu.github.io

Personal academic homepage of Jiafeng Xu — <https://simanxu.github.io>

A single hand-written static page. No Jekyll, no build step: edit `index.html`, commit, push,
and GitHub Pages serves it directly (`.nojekyll` disables Jekyll processing).

```
index.html        the whole site (inline CSS + content: About / News / Publications / Projects / Awards)
images/           portrait, favicons, full-size figures
images/teaser/    compressed thumbnails actually used by the page (~60-130 KB each)
files/            paper PDFs
```

## How to update

**Preview locally:** open `index.html` in a browser (double-click), or `python3 -m http.server` in this folder.

**Add a news item** — in the `<section id="news">` list, newest first:

```html
<li><span class="date">[2026/09]</span> Some news, with a <a href="https://...">link</a>.</li>
```

**Add a publication** — copy a `<div class="pub">` block inside `<section id="publications">`.
With a teaser image:

```html
<div class="pub">
  <div class="teaser"><a href="PROJECT_URL"><img src="images/teaser/NAME.jpg" alt="NAME"></a></div>
  <div>
    <div class="pub-title">Paper Title</div>
    <div class="authors">A. Author, <b>Jiafeng Xu</b>, C. Author</div>
    <div class="venue">Venue (ACRONYM), 2026</div>
    <div class="links">[<a href="files/FILE.pdf">PDF</a>] [<a href="https://arxiv.org/abs/...">arXiv</a>]
      [<a href="https://github.com/...">Code</a>] [<a href="PROJECT_URL">Website</a>]</div>
    <div class="award">Best Paper Award</div>   <!-- optional -->
  </div>
</div>
```

Without a figure, replace the teaser with the text placeholder:

```html
<div class="teaser"><a href="..."><div class="ph">ICRA<br>2026</div></a></div>
```

PDF file names containing spaces must be URL-encoded in `href` (space → `%20`).

**Add a project card** — copy a `<div class="card">` block inside `<section id="projects">`.

**New figures:** keep the original in `images/` and generate the thumbnail the page loads with

```bash
sips -s format jpeg -s formatOptions 72 -Z 720 images/NEW.png --out images/teaser/NEW.jpg
```

**Bilingual About:** English text lives in `#about-en`, Chinese in `#about-zh`; the 中文/EN button
toggles between them. Edit both when the bio changes.
