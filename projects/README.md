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

## Images and assets in the project page

Add images anywhere in your project markdown using standard syntax. Use relative paths (e.g. `./file.jpg` or `file.jpg`); they resolve to the project folder.

```markdown
![Robot setup](./vellai_kunjan_2.jpg)

Your project description here...
```

The **first image** in the body is shown large (hero-style) at the top of the project page. Other images and links (e.g. `[Download PDF](./report.pdf)`) use the same relative paths and work as usual.
