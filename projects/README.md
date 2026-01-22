# Projects

This folder contains all project markdown files.

## Adding a New Project

1. Create a new markdown file: `projects/<slug>.md`
   - Use a simple slug (e.g., `my-robot.md`, `web-app.md`)
   
2. Add frontmatter at the top:
   ```markdown
   ---
   title: "Your Project Title"
   date: "Nov 2024 - Dec 2024"
   summary: "A short one- or two-line summary shown on the projects index."
   ---
   ```

3. Write your full project description below the frontmatter using Markdown.

4. Add the slug to `projects/index.json`:
   ```json
   ["example", "my-robot"]
   ```

That's it! The project will automatically appear on the projects index page and be accessible at `projects/project.html?slug=<slug>`.

## File Structure

- `index.json` - List of project slugs (filename without `.md`)
- `<slug>.md` - One markdown file per project with frontmatter + content
- `project.html` - Generic page that renders any project's markdown
