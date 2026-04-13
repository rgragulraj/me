# Projects

Each project lives in its own folder under `projects/`. The folder holds the project markdown file and any assets (images, etc.).

## Adding a New Project

1. Create a project folder: `projects/<slug>/`
   - Use a simple slug (e.g., `lerobot`, `my-robot`, `web-app`).

2. Create the markdown file: `projects/<slug>/<slug>.md`
   - Example: `projects/lerobot/lerobot.md`

3. Add frontmatter at the top:

   ```markdown
   ---
   title: "Your Project Title"
   date: "Nov 2024 - Dec 2024"
   summary: "A short one- or two-line summary shown on the projects index."
   image: "card.jpg"
   ---
   ```

   - `title`, `date`, and `summary` are required for the index page.
   - `image` is optional. Filename of an image in the project folder shown on the **projects index** (projectshome) card.

4. Write your full project description below the frontmatter using Markdown.

5. Add the slug to `projects/index.json`:

   ```json
   ["lerobot", "my-robot"]
   ```

That's it! The project will appear on the projects index page and be accessible at `projects/project.html?slug=<slug>`.

## Project Folder Structure

```text
projects/
  index.json           # List of project slugs
  project.html         # Generic page that renders any project's markdown
  lerobot/
    lerobot.md         # Project content (required)
    image.png          # Optional: images, diagrams, etc.
    other-assets/      # Optional: subfolders for assets
  my-robot/
    my-robot.md
    ...
```

- **`<slug>/<slug>.md`** – Required. One markdown file per project with frontmatter + content.
- **`<slug>/*`** – Optional. Store images, PDFs, or other assets here. Reference them in markdown as `./image.png` or `image.png`; they will be loaded from the project folder.

## Images and assets in the project page

Add images anywhere in your project markdown using standard syntax. Use relative paths (e.g. `./file.jpg` or `file.jpg`); they resolve to the project folder.

```markdown
![Robot setup](./example.jpg)

Your project description here...
```

The **first image** in the body is shown large (hero-style) at the top of the project page. Other images and links (e.g. `[Download PDF](./report.pdf)`) use the same relative paths and work as usual.

## Videos (YouTube embeds + local video files)

### YouTube (recommended)

Use an `<iframe>` embed anywhere in the markdown body (raw HTML is supported).

```html
<div style="aspect-ratio: 16/9; width: 100%; margin: 1rem 0;">
  <iframe
    src="https://www.youtube.com/embed/VIDEO_ID?autoplay=1&mute=1&playsinline=1"
    title="Demo video"
    style="width:100%;height:100%;border:none;border-radius:8px;"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
  ></iframe>
</div>
```

### Local video files (`.mp4`, `.webm`)

Put the video file inside the project folder and reference it with a relative path.

```html
<video controls playsinline style="width: 100%; border-radius: 8px; margin: 1rem 0;" src="./demo.mp4"></video>
```

## Carousel (images + videos) — copy/paste template

Carousels are implemented directly in the project markdown using raw HTML: a wrapper `<div>`, a set of “slide” elements (images/iframes/videos), and two buttons with a small inline `onclick` script.

### Rules

- **One carousel wrapper**: `<div class="<name>-carousel" data-carousel-index="0" ...>`
- **All slides share one class**: e.g. `.carousel-slide` (or `<name>-slide`)
- **Update the slide count** in both button handlers:
  - In “Previous”: `...-1+N)%N`
  - In “Next”: `...+1)%N`
- **Start with slide 0 visible** and the rest with `display:none;`
- **Images inside the carousel** should use `src="./file.png"` (relative to the project folder)

### Template (2 slides)

```html
<div class="my-carousel" data-carousel-index="0" style="position: relative; display: flex; align-items: center; gap: 0.75rem; width: 100%; max-width: 100%; margin: 1rem 0;">
  <button type="button" aria-label="Previous"
    onclick="var c=this.parentNode;var s=c.querySelectorAll('.carousel-slide');var i=(parseInt(c.getAttribute('data-carousel-index'),10)-1+2)%2;c.setAttribute('data-carousel-index',i);s.forEach(function(el,j){el.style.display=j===i?'block':'none';});"
    style="flex-shrink:0;width:36px;height:36px;border-radius:50%;border:1px solid rgba(255,255,255,0.4);background:rgba(255,255,255,0.1);color:#fff;font-size:1.25rem;cursor:pointer;display:flex;align-items:center;justify-content:center;">‹</button>

  <div style="flex: 1; width: 100%; min-width: 0; aspect-ratio: 16/9; background: rgba(255,255,255,0.06); border-radius: 8px; overflow: hidden; position: relative;">
    <div class="carousel-slide" style="width:100%;height:100%;position:absolute;inset:0;">
      <img src="./slide_1.png" alt="Slide 1" style="width:100%;height:100%;object-fit:contain;border-radius:8px;" />
    </div>
    <div class="carousel-slide" style="width:100%;height:100%;position:absolute;inset:0;display:none;">
      <iframe src="https://www.youtube.com/embed/VIDEO_ID?autoplay=1&mute=1&playsinline=1" title="Slide 2 video"
        style="width:100%;height:100%;border:none;border-radius:8px;"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen></iframe>
    </div>
  </div>

  <button type="button" aria-label="Next"
    onclick="var c=this.parentNode;var s=c.querySelectorAll('.carousel-slide');var i=(parseInt(c.getAttribute('data-carousel-index'),10)+1)%2;c.setAttribute('data-carousel-index',i);s.forEach(function(el,j){el.style.display=j===i?'block':'none';});"
    style="flex-shrink:0;width:36px;height:36px;border-radius:50%;border:1px solid rgba(255,255,255,0.4);background:rgba(255,255,255,0.1);color:#fff;font-size:1.25rem;cursor:pointer;display:flex;align-items:center;justify-content:center;">›</button>
</div>
```
