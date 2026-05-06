# Pagina contatti stile Pokémon

Landing page mobile-first da hostare su GitHub Pages e linkare via chip NFC nascosto sotto una Pokéball.

## Struttura

- `index.html` — la pagina (singolo file, nessuna dipendenza)
- `blaine-avatar.png` — avatar trainer (256×256, sfondo bianco)
- `arcanine.png` — sprite Pokémon che cammina nella barra in fondo (64×64, sfondo trasparente)
- `erba.png` — tile del terreno (96×96, ripetuto in orizzontale)

## 1. Banner

- Dimensione del contenitore: **480×200 px** (mobile-first, max-width 480)
- Per mettere un banner: salva un file chiamato **`banner.png`** nella stessa cartella di `index.html`. Viene caricato automaticamente al posto del colore di default.
- L'immagine viene applicata con `background-size: cover`, quindi qualsiasi dimensione va bene — consigliato **1440×600 px** (ratio 12:5, retina-ready)
- Per cambiare il colore di fallback (quando non c'è `banner.png`): nel CSS `:root` cambia `--banner-color` e `--banner-color-2`

## 2. Replicare la pagina con altri trainer / Pokémon

Duplica la cartella e sostituisci 4 cose:

| Cosa | File / posizione | Note |
|---|---|---|
| Avatar | `blaine-avatar.png` | 256×256, sfondo bianco |
| Banner | `banner.png` | opzionale, qualsiasi dimensione (consigliato 1440×600) |
| Pokémon | `arcanine.png` | 64×64 trasparente, sprite frontale |
| Terreno | `erba.png` | 96×96 ripetibile (opzionale) |
| Testi | `index.html` | vedi sotto |

Nel file `index.html`:

- `<h1 id="full-name">` → nome e cognome
- `<strong id="role">` e `<span id="institution">` → ruolo / istituzione
- `href="tel:+39..."` → numero di telefono
- `href="https://instagram.com/..."` e `@username` → link e handle Instagram

**Direzione dello sprite:** Arcanine guarda a sinistra di default. Se carichi uno sprite che guarda a destra, nel `<script>` in fondo al file cambia:

```js
const NATURAL_FACES_LEFT = false;
```

## 3. Pubblicare su GitHub Pages (senza installare nulla)

1. Vai su [github.com](https://github.com) → **New repository** → nome es. `contatti` → spunta **Public** → **Create repository**
2. Nella pagina vuota clicca **"uploading an existing file"**
3. Trascina dentro tutti i file: `index.html`, `blaine-avatar.png`, `arcanine.png`, `erba.png`, `README.md`
4. Scrivi un messaggio di commit (es. "first") → **Commit changes**
5. Vai su **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**
6. Aspetta ~1 minuto → il sito è online su `https://TUOUSER.github.io/contatti/`

Per aggiornare: stessa repo → **Add file → Upload files** → sostituisci → commit.

### Alternativa: GitHub Desktop

1. Scarica [GitHub Desktop](https://desktop.github.com)
2. Login → **File → New repository** sulla cartella del progetto
3. Commit → **Publish repository**
4. Settings → Pages come sopra

## 4. Programmare il chip NFC

App consigliata: **NFC Tools** (Android Play Store / iOS App Store, gratis).

1. Apri NFC Tools → **Scrivi** → **Aggiungi un record**
2. Tipo: **URL/URI**
3. Incolla `https://TUOUSER.github.io/contatti/`
4. Tocca **Scrivi** e avvicina il chip al telefono

Il chip va incollato sotto la Pokéball; quando qualcuno avvicina il telefono si apre direttamente la pagina.

## Note tecniche

- Il bottone Instagram usa il gradiente ufficiale del brand
- Lo sprite Arcanine è vincolato alla larghezza esatta del bottone IG, ricalcolata su `resize` con `getBoundingClientRect()`
- Flip orizzontale automatico al cambio direzione (`scaleX(-1)`)
- Posizione fissa della barra in fondo (`position: fixed`)
- L'immagine del banner si imposta salvando un file `banner.png` nella cartella del progetto (rilevamento automatico al caricamento)
