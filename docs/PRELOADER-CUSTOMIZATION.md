# Preloader Customization Guide

Ovaj fajl objašnjava kako da prilagodite preloader animaciju na vašem sajtu.

## Fajlovi

- **preloader-demo.html** - Standalone demo fajl sa kompletnom preloader animacijom
- **CSS stilovi** - Nalaze se u `css/styles.css` (linije 327-363)
- **JavaScript logika** - Nalazi se u `js/main.js` (linije 59-117)

## Šta možete menjati

### 1. Brzina animacije (JavaScript)

U `js/main.js`, funkcija `initPreloader()`:

```javascript
count += 5; // Povećaj ovaj broj za bržu animaciju (npr. 10, 20)
```

```javascript
}, 10); // Smanji ovaj broj za bržu animaciju (npr. 5, 1)
```

**Primer za bržu animaciju:**
```javascript
count += 10; // Skok od 10% umesto 5%
}, 5); // Interval od 5ms umesto 10ms
```

**Primer za sporiju animaciju:**
```javascript
count += 2; // Skok od 2% umesto 5%
}, 20); // Interval od 20ms umesto 10ms
```

### 2. Vreme pre nego što se preloader sakrije (JavaScript)

```javascript
setTimeout(() => {
  preloader.classList.add('hidden');
  // ...
}, 200); // Povećaj ovaj broj za duže čekanje (npr. 500, 1000)
```

### 3. Logo animacija (CSS)

U `css/styles.css`:

```css
.preloader-logo {
  animation: preloader-pulse 2s ease-in-out infinite;
  /* Promeni 2s za bržu/sporiju animaciju */
}
```

**Animacija pulsa:**
```css
@keyframes preloader-pulse {
  0%, 100% { 
    transform: scale(1);      /* Normalna veličina */
    opacity: 0.8;              /* Prozirnost */
  }
  50% { 
    transform: scale(1.05);    /* Povećaj za veći efekat (npr. 1.1, 1.2) */
    opacity: 1;                /* Potpuno vidljiv */
  }
}
```

### 4. Veličina i stil brojača (CSS)

```css
.preloader-counter {
  font-family: var(--font-body);
  font-size: clamp(80px, 15vw, 107px); /* Min: 80px, Ideal: 15vw, Max: 107px */
  color: var(--gold-primary);           /* Boja broja */
}
```

**Primeri:**
- Veći broj: `font-size: clamp(100px, 20vw, 150px);`
- Manji broj: `font-size: clamp(60px, 10vw, 80px);`
- Druga boja: `color: #FFFFFF;` ili `color: #B08F59;`

### 5. Pozadinska boja preloadera (CSS)

```css
.preloader {
  background: var(--black); /* Promeni u bilo koju boju */
}
```

**Primeri:**
- Bela: `background: #FFFFFF;`
- Zlatna: `background: #BC8B0B;`
- Gradijent: `background: linear-gradient(135deg, #000000 0%, #1a1a1a 100%);`

### 6. Brzina fade-out efekta (CSS)

```css
.preloader {
  transition: opacity 0.5s ease, visibility 0.5s ease;
  /* Promeni 0.5s za brži/sporiji fade-out */
}
```

**Primeri:**
- Brži: `transition: opacity 0.2s ease, visibility 0.2s ease;`
- Sporiji: `transition: opacity 1s ease, visibility 1s ease;`

### 7. Logo slika i veličina (HTML)

U svakom HTML fajlu:

```html
<img src="images/logo-skaska.png" 
     alt="Skaska" 
     class="preloader-logo" 
     style="width: 60px; height: 60px; margin-bottom: 20px; opacity: 0.8;">
```

**Možete promeniti:**
- `width` i `height` - veličina loga
- `margin-bottom` - razmak između loga i brojača
- `opacity` - početna prozirnost (0.0 - 1.0)

### 8. Zvuk (JavaScript)

```javascript
pouringSound.volume = 0.5; // Promeni na 0.0-1.0 (0 = tiho, 1 = glasno)
```

**Da isključite zvuk:**
- Uklonite pozive `playPouringSound()` i `stopPouringSound()`
- Ili postavite `volume = 0`

## Kako testirati promene

1. Otvorite `preloader-demo.html` u browseru
2. Napravite promene u CSS/JS
3. Osvežite stranicu (F5 ili Ctrl+R)
4. Za testiranje brzine, možete koristiti browser DevTools:
   - F12 → Network tab → Throttling → Slow 3G (da simulirate sporu vezu)

## Napomene

- Preloader se automatski sakriva kada stranica završi učitavanje
- Ako stranica već učitana, animacija će biti brža
- Zvuk se možda neće pustiti automatski zbog browser autoplay restrikcija
- Preloader blokira scroll dok je aktivan (`overflow: hidden`)

## Integracija u postojeće stranice

Preloader HTML se nalazi na svim stranicama:

```html
<!-- Preloader -->
<div class="preloader">
  <img src="images/logo-skaska.png" alt="Skaska" class="preloader-logo" style="width: 60px; height: 60px; margin-bottom: 20px; opacity: 0.8;">
  <span class="preloader-counter">0</span>
</div>
```

JavaScript se poziva u `main.js`:
```javascript
initPreloader();
```

CSS stilovi su u `styles.css` (linije 327-363).
