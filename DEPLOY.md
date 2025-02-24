# Návod na nasazení webu na GitHub Pages

## 1. Příprava repozitáře

1. Vytvořte nový repozitář na GitHubu
   - Přejděte na [GitHub](https://github.com)
   - Klikněte na "New repository"
   - Pojmenujte repozitář (např. `portfolio`)
   - Nastavte repozitář jako veřejný
   - Vytvořte repozitář

2. Propojte lokální projekt s GitHubem:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/VASE-USERNAME/NAZEV-REPOZITARE.git
   git push -u origin main
   ```

## 2. Konfigurace Astro

1. Upravte `astro.config.mjs`:
   - Nastavte `site` na vaši GitHub URL
   - Nastavte `base` na název vašeho repozitáře
   ```js
   export default defineConfig({
     site: 'https://vase-username.github.io',
     base: '/nazev-repozitare'
   });
   ```

## 3. Nastavení GitHub Actions

1. Vytvořte složku `.github/workflows` v kořenovém adresáři projektu
2. Vytvořte soubor `deploy.yml` s následujícím obsahem:
   ```yaml
   name: Deploy to GitHub Pages

   on:
     push:
       branches: [main]
     workflow_dispatch:

   permissions:
     contents: read
     pages: write
     id-token: write

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout
           uses: actions/checkout@v4
         - name: Setup Node
           uses: actions/setup-node@v4
           with:
             node-version: '18'
             cache: 'npm'
         - name: Install dependencies
           run: npm ci
         - name: Build
           run: npm run build
         - name: Upload Pages artifact
           uses: actions/upload-pages-artifact@v3
           with:
             path: dist

     deploy:
       needs: build
       runs-on: ubuntu-latest
       environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
       steps:
         - name: Deploy to GitHub Pages
           id: deployment
           uses: actions/deploy-pages@v4
   ```

## 4. Povolení GitHub Pages

1. Přejděte do nastavení vašeho repozitáře na GitHubu
2. V levém menu klikněte na "Pages"
3. V sekci "Build and deployment":
   - Source: nastavte na "GitHub Actions"

## 5. Nasazení webu

1. Commitněte a pushněte všechny změny:
   ```bash
   git add .
   git commit -m "Add GitHub Pages deployment"
   git push
   ```

2. Sledujte průběh nasazení:
   - Přejděte do záložky "Actions" ve vašem repozitáři
   - Počkejte na dokončení workflow
   - Po úspěšném nasazení bude web dostupný na:
     `https://vase-username.github.io/nazev-repozitare`

## Řešení problémů

- Pokud se web nezobrazuje správně, zkontrolujte:
  - Správnost nastavení `site` a `base` v `astro.config.mjs`
  - Zda jsou všechny cesty k obrázkům a souborům relativní k `base`
  - Zda je povolený GitHub Pages v nastavení repozitáře

- Pro lokální testování buildu:
  ```bash
  npm run build
  npm run preview
  ```