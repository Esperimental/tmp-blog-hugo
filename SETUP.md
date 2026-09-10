# Hugo prototype setup

1. Create a public repository and grant the GitHub connector access.
2. Add this source, including `.github/workflows/pages.yml`.
3. Select **Settings → Pages → Source → GitHub Actions**. It saves automatically.
4. Push to `main` or run the workflow. Rerun failed jobs if Pages was enabled after an initial failure.
5. Check both build and deploy jobs, then open the URL reported by deploy.
6. Check the home page, posts, images, stylesheet and navigation on desktop and phone.

The workflow downloads pinned Hugo 0.166.0, builds and checks repository-prefixed links, reads Pages settings, rebuilds with the actual base URL, uploads `public/` and deploys. It needs no npm install or Go compiler for this configuration. The check build happens before Pages configuration, allowing generator validation even if Pages setup is missing.

## Editing

Edit Markdown in `content/posts`, metadata in `hugo.toml` and `data/authors.json`, templates in `layouts`, and CSS in `assets/style.css`. Commit source, not generated `public/`.

A text-only post can remain `content/posts/slug.md`. For a post with local images, make a page bundle:

```text
content/posts/slug/
├── index.md
└── descriptive-name.webp
```

Use normal Markdown in `index.md`:

```md
![Descriptive alternative text](descriptive-name.webp "Optional caption")
```

The render hook in `layouts/_markup/render-image.html` finds the bundled image, emits its width and height, lazy-loads it and uses the Markdown title as a caption. Prefer lowercase descriptive filenames. Resize generated originals to the largest useful display size and export as WebP before committing; the current test image is 1400 pixels wide and about 100 KB.

The CSS is processed by Hugo, minified and fingerprinted. The changing filename prevents a newly deployed page from loading an older cached stylesheet.

## Local checks

```sh
hugo --baseURL https://example.test/tmp-blog-hugo/
python3 scripts/check-output.py public /tmp-blog-hugo/
hugo server
```

The checker validates generated HTML and local references, including fingerprinted CSS and bundled images. `scripts/editorial-trials.py` also builds temporary content variations so template assumptions are tested without keeping those posts.

## Promoting the experiment

Use this temporary repository as staging for template, workflow and content-pipeline changes. When transferring a proven change to `blog`, update source-repository links in templates, content and docs. Deployment URLs derive from Pages automatically. The eventual root `site` remains a separate repository and can link to the blog and other projects.

Reference: https://gohugo.io/host-and-deploy/host-on-github-pages/
