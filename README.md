# ⚛ Escher z^c Transformatie

Een interactieve p5.js web-app die de complexe machtsverheffing **f(z) = z^c** pixel-voor-pixel toepast op een afbeelding — geïnspireerd op Eschers "Print Gallery"-werken.

🌐 **Live demo:** https://&lt;jouw-gebruikersnaam&gt;.github.io/p5js-escher-transform/

---

## Hoe het werkt

De app heeft drie panelen naast elkaar:

| Paneel | Functie |
|--------|---------|
| **① C-selector** | Complexe vlak (−2.5 tot 2.5 op beide assen). Klik of sleep om de constante `c = a + bi` te kiezen. |
| **② Upload** | Laad een eigen afbeelding als bronmateriaal. |
| **③ Resultaat** | Toont de getransformeerde afbeelding via inverse sampling. |

### De transformatie: f(z) = z^c

Voor elke uitvoerpixel `(px, py)`:

1. **Map** coördinaat naar complex getal `z = x + yi` (complex vlak −2.5…2.5)
2. **Bereken** `w = z^c` via complexe exponentieel:

   ```
   z^c = exp(c · ln z)
   ln z = ln|z| + i·arg(z)
   c · ln z = (a·ln|z| − b·θ) + i·(b·ln|z| + a·θ)
   ```

3. **Sample** de bronafbeelding op de positie die overeenkomt met `w` (inverse mapping)

### Interessante waarden voor c

| c | Effect |
|---|--------|
| `2 + 0i` | Kwadratische mapping (Joukowski-achtig) |
| `0.5 + 0i` | Vierkantswortel — vouwt de afbeelding |
| `1 + 1i` | Spiraalvorm |
| `0 + 1i` | Puur imaginair — rotatiesymmetrie |
| `−1 + 0i` | Inversie (z → 1/z) |
| `0.5 + 0.5i` | Escher-achtig spiraaleffect |

---

## Techniek

- **Geen build tools** — enkelvoudig `index.html`
- **p5.js via CDN** voor de C-selector canvas
- **Vanilla Canvas 2D API** voor pixel-manipulatie (ImageData)
- **Werkt lokaal** — open `index.html` direct in de browser

---

## Lokaal draaien

```bash
# Geen installatie nodig — open gewoon het bestand:
start index.html

# Of met een lokale server (bijv. voor strikte browsers):
npx serve .
python -m http.server 8080
```

---

## GitHub Pages deployen

```bash
# 1. Initialiseer git-repo (eenmalig)
git init
git add .
git commit -m "feat: initial Escher z^c transform app"

# 2. Maak nieuwe GitHub-repo aan en push
gh repo create p5js-escher-transform --public --source=. --remote=origin --push

# 3. Activeer GitHub Pages (main branch, root /)
gh api --method POST /repos/$(gh api /user --jq .login)/p5js-escher-transform/pages \
  --field source='{"branch":"main","path":"/"}'

# 4. Bekijk de live URL
gh browse --repo p5js-escher-transform
```

> Na activering is de app doorgaans binnen 1–2 minuten live op  
> `https://<gebruikersnaam>.github.io/p5js-escher-transform/`

---

## Licentie

MIT — vrij te gebruiken en aanpassen.
