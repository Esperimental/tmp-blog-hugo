# Hugo blog experiment

Matching prototype for [the Eleventy experiment](https://github.com/Esperimental/tmp-blog-eleventy).

Same two posts and author data; Hugo templates replace Nunjucks. No external theme, npm packages, Sass or Go modules.

Requires Hugo 0.166.0 (the standard Linux binary works).

```sh
hugo --baseURL https://example.test/tmp-blog-hugo/
python3 scripts/check-output.py public /tmp-blog-hugo/
hugo server
```

Select **Settings → Pages → Source → GitHub Actions** once. Push to main to publish; pull requests build without deploying.

- Posts: `content/posts/`
- Settings: `hugo.toml`
- Authors: `data/authors.json`
- Layouts: `layouts/`
- CSS source: `assets/style.css`
- Workflow: `.github/workflows/pages.yml`

The stylesheet is minified and fingerprinted during the build so browsers do not keep stale CSS after a deployment.

Posts without local media can be single Markdown files. Posts with images use a leaf bundle:

```text
content/posts/my-post/
├── index.md
└── image.webp
```

Reference the image with ordinary Markdown:

```md
![Useful alt text](image.webp "Optional visible caption")
```

The custom Markdown image renderer resolves the adjacent page resource and adds intrinsic dimensions, lazy loading and the optional caption. This keeps post content portable and avoids shortcode syntax for normal images.

[Setup guide](SETUP.md). Branding and the second sample post remain provisional.
