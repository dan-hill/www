## www

`www` is the public-facing Hugo site repo in the current multi-repo stack.

### Module identity

- Module path: `github.com/dan-hill/www`

### Dependency chain

`www` imports `github.com/dan-hill/site-base`, and `site-base` imports `github.com/dan-hill/ox`.

That means the visual stack for `www` is:

- `www` → `site-base` → `ox`

### Content sources

- author Org sources in `content-org/`
- commit exported Markdown in `content/`

### GitHub Pages workflow note

The workflow at `.github/workflows/deploy-pages.yml` already sets up Go and Hugo and builds from the site root.

For that workflow to succeed after the new OX integration, OpenClaw must first ensure:

1. `github.com/dan-hill/ox` is pushed and tagged
2. `github.com/dan-hill/site-base` is updated to that OX tag and pushed/tagged
3. `www` is updated to the intended `site-base` tag with:
   - `hugo mod get github.com/dan-hill/site-base@<tag>`
4. the resulting `go.mod` and `go.sum` updates are committed before Pages deploy runs

Because OX ships precompiled runtime CSS, the current Pages workflow does not need Hugo extended just to render the shared theme.