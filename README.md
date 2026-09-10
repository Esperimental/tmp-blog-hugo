# Hugo blog experiment

Matching prototype for [the Eleventy experiment](https://github.com/Esperimental/tmp-blog-eleventy).

Same two posts, author data and CSS; Hugo templates replace Nunjucks. No external theme, npm packages, Sass or Go modules.

Requires Hugo 0.166.0 (standard Linux binary works).

```sh
hugo --baseURL https://example.test/tmp-blog-hugo/
python3 scripts/check-output.py public /tmp-blog-hugo/
hugo server
```

Select **Settings → Pages → Source → GitHub Actions** once. Push to main to publish; pull requests build without deploying.

- Posts: content/posts/
- Settings: hugo.toml
- Authors: data/authors.json
- Layouts: layouts/
- CSS: static/assets/style.css
- Workflow: .github/workflows/pages.yml

[Setup guide](SETUP.md). Branding and the second sample post remain provisional.
