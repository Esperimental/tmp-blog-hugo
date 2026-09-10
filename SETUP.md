# Hugo prototype setup

1. Create a public repository and grant the GitHub connector access.
2. Add this source, including .github/workflows/pages.yml.
3. Select **Settings → Pages → Source → GitHub Actions**. It saves automatically.
4. Push to main or run the workflow. Rerun failed jobs if Pages was enabled after an initial failure.
5. Check both build and deploy jobs, then open the URL reported by deploy.
6. Check home, posts, stylesheet and navigation on desktop and phone.

The workflow downloads pinned Hugo 0.166.0, builds and checks repository-prefixed links, reads Pages settings, builds with the actual base URL, uploads public/ and deploys. It needs no npm install or Go compiler for this configuration. The check build happens before Pages configuration, allowing generator validation even if Pages setup is missing.

Edit Markdown in content/posts, metadata in hugo.toml and data/authors.json, templates in layouts, and CSS in static/assets. Commit source, not generated public/.

Local build: `hugo --baseURL https://example.test/tmp-blog-hugo/`.
Check: `python3 scripts/check-output.py public /tmp-blog-hugo/`.
Preview: `hugo server`.

When transferring to blog, update source-repository links in templates/content/docs. Deployment URLs derive from Pages automatically. An eventual root site remains a separate site repository.

Reference: https://gohugo.io/host-and-deploy/host-on-github-pages/
