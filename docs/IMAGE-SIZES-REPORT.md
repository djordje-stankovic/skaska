# Poređenje veličina slika – trenutno vs preporučeno

## Legenda
- **Preporuka:** dimenzije (širina×visina) i okvirna veličina fajla
- **Prioritet:** 🔴 visok (preveliko / sporo) | 🟡 umereno | 🟢 OK

---

## Slike za deljenje (og:image / Facebook, Viber)

| Slika | Trenutno | Preporuka | Prioritet |
|-------|----------|-----------|-----------|
| **brandy-glass.jpg** | 978×1280, **52 KB** | 1200×630 px, 200–400 KB | 🟡 Dimenzije nisu idealne za og (FB preferira 1200×630). Fajl je mali – OK. |

---

## Hero / pozadine stranica

| Slika | Trenutno | Preporuka | Prioritet |
|-------|----------|-----------|-----------|
| **hero-commitment.jpg** | 1920×1280, **363 KB** | max 1920 px, ~200–300 KB | 🟢 Blago iznad – može blaga kompresija |
| **hero-contact.jpg** | 1920×1280, **436 KB** | max 1920 px, ~200–300 KB | 🟡 Smanjiti na ~250–300 KB |
| **hero-distillery.jpg** | 800×1200, **257 KB** | max 1920 px | 🟢 OK |
| **hero-gallery.jpg** | 1920×1280, **413 KB** | max 1920 px, ~200–300 KB | 🟡 Smanjiti na ~250–300 KB |
| **VAL041511.jpg** (news hero) | 2000×1500, **860 KB** | max 1920 px, ~300 KB | 🔴 Smanjiti rezoluciju i kompresiju |
| **VAL04129.jpg** (where-to-buy hero) | 2000×2000, **1117 KB** | max 1920 px, ~300 KB | 🔴 Smanjiti rezoluciju i kompresiju |
| **DJI_0865.JPG** (sr about hero) | 5472×3078, **6.5 MB** | max 1920 px, ~300 KB | 🔴 Mnogo preveliko – prioritet za kompresiju |

---

## About stranica – mediji

| Slika | Trenutno | Preporuka | Prioritet |
|-------|----------|-----------|-----------|
| **MarkoSlika.png** | 895×499, **791 KB** | 800–1200 px širine, JPG ~150 KB | 🔴 PNG prevelik – konvertovati u JPG i kompresovati |
| **Andrej.JPG** | 5616×3744, **5.3 MB** | max 1200 px širine, ~200 KB | 🔴 Mnogo preveliko |
| **gallery/Destilacija.JPG** | 6720×4480, **7.8 MB** | max 1200 px, ~200 KB | 🔴 Mnogo preveliko |
| **gallery/292A9390.JPG** | 6720×4480, **5.1 MB** | max 1200 px, ~200 KB | 🔴 Mnogo preveliko |
| **gallery/DJI_0828.JPG** | 5472×3078, **7 MB** | max 1200 px | 🔴 Mnogo preveliko |
| **gallery/Kazan 1000l.jpg** | 4480×6720, **1.9 MB** | max 1200 px | 🔴 Smanjiti |
| **gallery/Podrum.jpg** | 4096×2160, **1.3 MB** | max 1200 px | 🔴 Smanjiti |
| Ostale gallery/*.JPG | 5472–6720 px, **6–11 MB** svaka | max 1200 px, ~150–250 KB | 🔴 Sve prevelike |

---

## News – kartice vesti

| Slika | Trenutno | Preporuka | Prioritet |
|-------|----------|-----------|-----------|
| **LSC_25.JPG** | 918×872, **128 KB** | 800–1200 px, &lt;200 KB | 🟢 OK |
| **unnamed.jpg** | 1179×782, **133 KB** | isto | 🟢 OK |
| **top-5-brandies.jpg** | 1080×1080, **161 KB** | isto | 🟢 OK |
| **IMG_4742-1.jpg** | –, **186 KB** | isto | 🟢 OK |
| **SharedScreenshot.jpg** | –, **16 KB** | isto | 🟢 OK |
| **skaska-u-londonu.jpg** | –, **80 KB** | isto | 🟢 OK |
| **usr-silver-medal.jpg** | –, **157 KB** | isto | 🟢 OK |
| **rakija-podcast.jpg** | –, **201 KB** | isto | 🟢 OK |
| **Balkan Spirits Gold.jpg** | –, **660 KB** | &lt;200 KB | 🟡 Može kompresija |

---

## Ostalo (logotipi, medalje, certifikati)

| Slika | Trenutno | Napomena |
|-------|----------|----------|
| logo/*.png, Skaska-white.png, medal-*.png | 12–93 KB | 🟢 OK, male ikone |
| medals/balkan_competition.png | **931 KB** | 🟡 Može smanjenje (npr. PNG optim ili JPG ako nema providnost) |
| Skaska-vratnice.png | **161 KB** | 🟢 Prihvatljivo |
| IMG_0978.jpg (certifikat) | **65 KB** | 🟢 OK |

---

## Rezime

| Kategorija | Broj slika | Akcija |
|------------|------------|--------|
| 🔴 **Visok prioritet** (prevelike, spore) | ~15+ | Hero DJI_0865, Andrej, cela gallery/, VAL04129, VAL041511, MarkoSlika.png – smanjiti rezoluciju (npr. max 1920 px za hero, max 1200 px za sadržaj) i JPG kvalitet ~82%. |
| 🟡 **Srednji prioritet** | ~5 | Hero commitment/contact/gallery, Balkan Spirits Gold – blaga kompresija. brandy-glass – opciono napraviti verziju 1200×630 za og. |
| 🟢 **OK** | News kartice, logotipi, hero-distillery, LSC_25, itd. | Nema hitne izmene. |

**Preporučene dimenzije ukratko:**
- **og:image (deljenje):** 1200×630 px, JPG, 200–400 KB  
- **Hero pozadine:** max 1920 px širine, JPG, 200–350 KB  
- **Sadržaj (about, galerija):** max 1200 px širine, JPG, 150–250 KB  
- **News kartice:** 800–1200 px, &lt;200 KB – većina je već u redu  

Ako želiš, sledeći korak može biti skripta za kompresiju (npr. Node + sharp) ili konkretne ffmpeg/ImageMagick komande za ove fajlove.
