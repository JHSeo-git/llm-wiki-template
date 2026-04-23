## Deploy Quartz site to GitHub Pages

**`.github/workflows/deploy.yml`**:

```yaml
name: Deploy Quartz site to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

env:
  QUARTZ_REF: v4.5.2 # Pin Quartz version (tag/branch/commit hash all supported)
  CONTENT_FOLDER: wiki # The folder containing the content to be deployed

jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - name: Checkout site repo
        uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Needed for git-based timestamps

      - name: Checkout Quartz
        uses: actions/checkout@v4
        with:
          repository: jackyzha0/quartz
          ref: ${{ env.QUARTZ_REF }}
          path: quartz

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: npm
          cache-dependency-path: quartz/package-lock.json

      - name: Apply custom config & assets
        run: |
          set -e
          cp .github/quartz/quartz.config.ts quartz/quartz.config.ts
          cp .github/quartz/quartz.layout.ts quartz/quartz.layout.ts

          if [ -f .github/quartz/custom.scss ]; then
            cp .github/quartz/custom.scss quartz/quartz/styles/custom.scss
          fi

          if [ -d .github/quartz/static ]; then
            cp -r .github/quartz/static/* quartz/quartz/static/
          fi

          rm -rf quartz/content
          ln -s "$GITHUB_WORKSPACE/$CONTENT_FOLDER" quartz/content

      - name: Install dependencies
        working-directory: quartz
        run: npm ci

      - name: Build Quartz
        working-directory: quartz
        run: npx quartz build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: quartz/public

  deploy:
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

## Preflight Checklist

1. **Repository structure**

   ```
   my-vault/
   ├── wiki/                           # Notes to publish with Quartz
   └── .github/
       ├── workflows/deploy.yml        # This file
       └── quartz/
           ├── quartz.config.ts
           ├── quartz.layout.ts
           ├── custom.scss             # Optional
           └── static/                 # Optional (favicon, etc.)
   ```

   If your published content lives somewhere else, update `CONTENT_FOLDER` in `.github/workflows/deploy.yml`.

2. **GitHub Pages Setup**
   Change Settings → Pages → Source to **"GitHub Actions"** (not the default "Deploy from a branch")

3. **Prepare Quartz config files**
   - Copy `quartz.config.ts` and `quartz.layout.ts` from the `jackyzha0/quartz` repo into `.github/quartz/`, then customize them
   - Set `baseUrl` to the actual deployment domain (for example, `your-username.github.io/repo-name` or a custom domain)

4. **Branch name**
   `on.push.branches` is set to `[main]`; adjust it to match the default branch name of your vault repo (`master` if that is what you use)

## Upgrade & Rollback

Quartz version management is handled entirely through the `QUARTZ_REF` env value:

```yaml
env:
  QUARTZ_REF: v4.5.2 # Stable version
  # QUARTZ_REF: v4        # Always follow the latest v4 (not recommended)
  # QUARTZ_REF: 3a1b2c4   # Pin a specific commit
```

Strongly recommend pinning to a tag. Tracking the `v4` branch can pull in upstream breaking changes without notice and break CI. Check the latest tags at [jackyzha0/quartz/releases](https://github.com/jackyzha0/quartz/releases).
