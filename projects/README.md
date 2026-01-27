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
   image: "hero.jpg"
   ---
   ```
   
   - `title`, `date`, and `summary` are required for the index page.
   - `image` is optional. If provided, it should be the filename of an image in the project folder (e.g., `"hero.jpg"`). The image will be displayed on the projects index page.

4. Write your full project description below the frontmatter using Markdown.

5. Add the slug to `projects/index.json`:
   ```json
   ["lerobot", "my-robot"]
   ```

That's it! The project will appear on the projects index page and be accessible at `projects/project.html?slug=<slug>`.

## Project Folder Structure

```
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

## Referencing Assets in Markdown

Inside your project markdown, use relative paths for assets in the same folder:

```markdown
![Robot setup](./setup.jpg)
[Download report](./report.pdf)
```

These resolve to `projects/<slug>/setup.jpg` and `projects/<slug>/report.pdf` on the project page.
