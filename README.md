
Tento postup je užitečný za předpokladu, že dokážeme pushnout repozitář na svůj GH účet.

# Před pushováním do repozitáře na svém GH účtu
1. V souboru .gitignote zakomentujeme pomocí znaku # řádek č. 3, na kterém se nachází package-lock.json

2. V souboru vite.config.js před řádek č. 5 (root: './src') přidáme řádek base: '/name-repository/' a názvem svého repozitáře, na kterém chceme deploy GH Pages, v mém případě gh-pages base: '/gh-pages/'.
Dále v tomto souboru přidáme 2 tečky .. u publicDir, což znamená, půjdeme o adresář výše
publicDir: '../../public',

# Po úspěšném pushnutí svého repozitáře na GH
1. V nastavení svého repozitáře přes Setting > Pages > 

.github/workflows/main.yml

obsah 

# Simple workflow for deploying static content to GitHub Pages
name: Deploy static content to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ['main']

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets the GITHUB_TOKEN permissions to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow one concurrent deployment
concurrency:
  group: 'pages'
  cancel-in-progress: true

jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Set up Node
        uses: actions/setup-node@v3
        with:
          node-version: 18
          cache: 'npm'
      - name: Install dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          # Upload dist repository
          path: './dist'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2


U About klikneme na nastavení, označíme radio button () a uložíme.

Nyní se můžeme těšit ze svého projektu, který jsme dokázaly publikovat přes GH Pages.