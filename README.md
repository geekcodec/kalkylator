# ROI-kalkylator

En inbäddningsbar ROI-kalkylator för svenska soloprenörer och småföretagare. Beräkna intäkter och lönsamhet baserat på leads, konverteringsgrad, produktpris och annonskostnader.

## 📋 Funktioner

- **4 inmatningsfält**: Leads, konverteringsgrad, produktpris, annonskostnad
- **3 valutor**: SEK, USD, EUR med korrekt formatering
- **7 beräknade metrics**: Kunder, intäkt, nettointäkt, ROI, kostnad per lead, CAC
- **Real-time beräkningar**: Uppdateras automatiskt med 300ms debounce
- **Visuell feedback**: Grön/röd indikering för positiv/negativ ROI
- **Responsiv design**: Fungerar på mobil, tablet och desktop
- **Tillgänglighet**: ARIA-attribut, keyboard navigation, semantisk HTML

## 🚀 Snabbstart

### Alternativ 1: Öppna direkt

Öppna `roi-kalkylator.html` i valfri webbläsare.

### Alternativ 2: Lokal server

```bash
# Med Python 3
python3 -m http.server 8000

# Med Node.js
npx serve .
```

Besök sedan `http://localhost:8000/roi-kalkylator.html`

## 📦 Inbäddning

### Via iframe

```html
<iframe 
  src="https://din-domain.se/roi-kalkylator.html" 
  width="100%" 
  height="800" 
  frameborder="0"
  style="max-width: 600px; margin: 0 auto; display: block;">
</iframe>
```

### Direkt inbäddning

Kopiera hela innehållet i `roi-kalkylator.html` direkt till din webbsida. Filen är helt fristående utan externa beroenden.

#### WordPress

1. Skapa en ny sida
2. Byt till "Text" eller "HTML" läge
3. Klistra in hela HTML-koden
4. Spara och publicera

#### Squarespace / Wix

1. Lägg till ett "Code" eller "HTML"-block
2. Klistra in hela HTML-koden
3. Spara

## 🧮 Beräkningsformler

| Metric | Formel |
|--------|--------|
| Antal kunder | Leads × (Konverteringsgrad / 100) |
| Total intäkt | Antal kunder × Produktpris |
| Nettointäkt | Total intäkt - Annonskostnad |
| ROI (%) | ((Total intäkt - Annonskostnad) / Annonskostnad) × 100 |
| Kostnad per lead | Annonskostnad / Leads |
| CAC | Annonskostnad / Antal kunder |

## 💱 Valutaformatering

| Valuta | Format | Exempel |
|--------|--------|---------|
| SEK | Mellanslag + komma + "kr" efter | 1 997,50 kr |
| USD | Komma + punkt + "$" före | $1,997.50 |
| EUR | Mellanslag + komma + "€" före | €1 997,50 |

## 🎨 Anpassning

### Ändra färger

I `<style>`-taggen, sök efter dessa variabler:

```css
/* Primärfärg (iOS blå) */
#007AFF

/* Positiv/grön */
#34C759

/* Negativ/röd */
#FF3B30

/* Bakgrund */
#F5F5F7

/* Text primär */
#1D1D1F

/* Text sekundär */
#6E6E73
```

### Ändra typsnitt

```css
font-family: 'Ditt typsnitt', -apple-system, BlinkMacSystemFont, ...;
```

### Lägga till dark mode

Lägg till följande CSS i slutet av `<style>`-taggen:

```css
@media (prefers-color-scheme: dark) {
  body {
    background: #000000;
    color: #FFFFFF;
  }
  
  .calculator-form {
    background: #1C1C1E;
  }
  
  input[type="number"] {
    background: #2C2C2E;
    color: #FFFFFF;
    border-color: #3A3A3C;
  }
  
  /* ... mer dark mode styling */
}
```

## ✅ Browser-stöd

- Chrome (desktop & mobil)
- Safari (desktop & iOS)
- Firefox
- Edge

## 📱 Responsiv design

- **Mobil** (< 768px): Full bredd med 16px padding
- **Tablet** (768px - 1024px): Max 600px, centrerat
- **Desktop** (> 1024px): Max 600px, centrerat

## ♿ Tillgänglighet

- Semantisk HTML med korrekta labels
- ARIA-attribut för skärmläsare
- Keyboard-navigation med piltangenter
- Focus-states för alla interaktiva element
- Minsta touch-target på 44x44px

## 🐛 Felsökning

### Resultat visas inte

Se till att alla fyra fält har värden. Resultat visas först när alla fält är ifyllda.

### Fel nummerformat

Kontrollera att rätt valuta är vald. SEK använder komma som decimaltecken, USD och EUR använder punkt.

### Layout ser fel ut på mobil

Se till att viewport meta-taggen finns:
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

## 📄 Licens

Fri att använda för personligt och kommersiellt bruk.

---

Skapad med ❤️ för svenska entreprenörer
