# hugo-mock-landing-page
Mock Landing page using Hugo

## Review left on github actions page:
I had no knowledge of what a workflow was before this doc, but now I understand it at a much higher level. This page was very informative and a good introduction to github actions and workflow functions

## Description of Workflow
This repository contains a mock landing page built with Hugo, with automated deployment to GitHub Pages using GitHub Actions.

### Deployment Workflow
This project uses GitHub Actions to automatically build and deploy the Hugo website to GitHub Pages whenever changes are pushed to the main branch. The workflow performs the following steps:

1. Checks out the repository code
2. Sets up Hugo environment (v0.144.1 extended)
3. Compiles the Hugo static files
4. Publishes the built site to the gh-pages branch

### Workflow Implementation
The workflow is defined in .github/workflows/gh-pages-deployment.yaml:
```
name: 🏗️ Build and Deploy GitHub Pages
on:
  push:
    branches:
      - main # Set a branch to deploy
jobs:
  deploy:
    runs-on: ubuntu-22.04
    steps:
      - name: 🔄 Check Out Source Repository
        uses: actions/checkout@v3.5.1
        with:
          submodules: true # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod
      - name: 🛠️ Initialize Hugo Environment
        uses: peaceiris/actions-hugo@v2.6.0
        with:
          hugo-version: "0.144.1"
          extended: true
      - name: 🏗️ Compile Hugo Static Files
        run: hugo -D --gc --minify
      - name: 🚀 Publish to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3.9.3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_branch: gh-pages
          user_name: "github-actions[bot]"
          user_email: "github-actions[bot]@users.noreply.github.com"
```

### Live Site
The live site is deployed at: https://[YOUR-GITHUB-USERNAME].github.io/hugo-mock-landing-page-autodeployed/

### Making Changes
Any changes pushed to the main branch will automatically trigger the GitHub Actions workflow to rebuild and redeploy the site. The workflow typically takes a few minutes to complete.
