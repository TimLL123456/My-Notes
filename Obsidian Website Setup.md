# Get Started
```bash
git clone https://github.com/jackyzha0/quartz.git
cd quartz
npm i
npx quartz create
```

# Building your Quartz
Once you’ve initialized Quartz, let’s see what it looks like locally:
```bash
npx quartz build --serve
```

# Setting up your GitHub repository
```bash
# list all the repositories that are tracked
git remote -v
 
# if the origin doesn't match your own repository, set your repository as the origin
git remote set-url origin https://github.com/TimLL123456/My-Notes.git
 
# if you don't have upstream as a remote, add it so updates work
git remote add upstream https://github.com/jackyzha0/quartz.git

npx quartz sync --no-pull
```

# Copy files
Copy files to `./quartz/content`

# Hosting
`quartz/.github/workflows/deploy.yml`
```bash
name: Deploy Quartz site to GitHub Pages
 
on:
  push:
    branches:
      - v4
 
permissions:
  contents: read
  pages: write
  id-token: write
 
concurrency:
  group: "pages"
  cancel-in-progress: false
 
jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Fetch all history for git info
      - uses: actions/setup-node@v4
        with:
          node-version: 22
      - name: Install Dependencies
        run: npm ci
      - name: Build Quartz
        run: npx quartz build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: public
 
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

<br>

Commit these changes
```bash
npx quartz sync
```