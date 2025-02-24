# Průvodce údržbou dokumentace

## Nástroje a integrace

### 1. Kontrola kvality

- **markdownlint**: Kontrola formátování a stylu
  - Konfigurace v `.markdownlint.json`
  - Spouštěno automaticky při každém commitu

- **markdown-link-check**: Validace odkazů
  - Kontroluje dostupnost všech URL
  - Detekuje rozbité odkazy

- **typos**: Kontrola pravopisu
  - Podporuje více jazyků
  - Možnost vlastního slovníku

### 2. Automatické generování obsahu

- **remark-toc**: Generování obsahu
  - Aktualizuje se automaticky při změnách
  - Zachovává strukturu nadpisů

- **shields.io**: Dynamické badges
  - Aktualizace stavu projektu
  - Metriky a statistiky

### 3. Integrační nástroje

#### Doporučené nástroje:

1. **Dependabot**
   - Automatické aktualizace závislostí
   - Konfigurace v `.github/dependabot.yml`

2. **CodeQL**
   - Analýza kvality kódu
   - Bezpečnostní kontroly

3. **Stale**
   - Správa neaktivních issues a PR
   - Automatické označování a zavírání

## Best Practices

1. **Struktura dokumentace**
   - Používejte konzistentní formátování
   - Dodržujte hierarchii nadpisů
   - Udržujte aktuální obsah

2. **Pravidelné revize**
   - Kontrolujte dokumentaci měsíčně
   - Aktualizujte příklady a screenshoty
   - Ověřujte platnost informací

3. **Verzování**
   - Označujte významné změny
   - Udržujte changelog
   - Dokumentujte breaking changes

## Proces aktualizace

1. **Denní automatizace**
   - Kontrola odkazů
   - Aktualizace badges
   - Generování TOC

2. **Týdenní kontroly**
   - Review pull requestů
   - Kontrola issues
   - Aktualizace examples

3. **Měsíční údržba**
   - Kompletní review dokumentace
   - Aktualizace verzí
   - Archivace zastaralého obsahu

## Řešení problémů

- **Rozbité odkazy**
  ```bash
  markdown-link-check README.md
  ```

- **Kontrola formátování**
  ```bash
  markdownlint "**/*.md"
  ```

- **Generování TOC**
  ```bash
  remark README.md -o --use toc
  ```