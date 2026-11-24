# Convenzioni del sito

Sito statico personale di Paolo, allenatore dei portieri. Pubblicato su GitHub Pages sotto
`https://<utente>.github.io/<repo>/`. Letto soprattutto da cellulare.

## Regole

- **Lingua del sito: spagnolo.** README e istruzioni in italiano.
- **Niente framework, niente build, niente npm.** Solo HTML + `assets/css/style.css` (unico CSS).
  Niente JavaScript: il menu mobile è un `<details class="menu">`.
- **Link relativi ovunque.** Mai percorsi che iniziano con `/` (il sito vive in una sottocartella).
- **Mobile first.** Verificare a 375px e 1280px.
- **Segnaposto:** i testi non ancora noti si scrivono `[__]` (o `[Rival]`, `[dd/mm/aaaa]`) e si
  avvolgono in `<span class="placeholder">` nelle pagine pubblicate. Non inventare dati, minuti,
  nomi o statistiche. Elencare i segnaposto rimasti a fine lavoro.
- **Niente trattini lunghi** (— o –) nei testi scritti per Paolo: usare virgole o frasi separate.
  Eccezione: il separatore del risultato (`2 – 3`, sempre squadra di casa a sinistra).
- **Menu:** quando si aggiunge una stagione, squadra o sezione, aggiornare il menu in **tutte** le
  pagine, template compreso.

## Naming

- Stagione: `temporada-AAAA-AA/`
- Squadra: `temporada-AAAA-AA/<club>/` (es. `apa-poble-sec`)
- Informe: `.../informes/AAAA-MM-GG-<rival>/` con `video/`, `poster/`, `img/`
- File media: `minXX.mp4`, `minXX.jpg` (minuto di gioco, due cifre: `min06`). Se non è un minuto: `clipXX`.
- Poster: stesso nome del video, `.jpg`, in `poster/`.
- Loghi: `assets/img/logos/<club>.png`

## Componenti (classi CSS)

- Scheda: `<section class="ficha">` con `<h2>` (maiuscolo via CSS) ed eventuale etichetta.
- Etichette (sempre con testo, non solo colore):
  - `<span class="etiqueta mejorar">A MEJORAR</span>` arancio `#F2913D`
  - `<span class="etiqueta bien">BIEN</span>` verde `#5FD39A`
  - `<span class="etiqueta sugerencia">SUGERENCIA</span>` giallo `#FFD84D`
- Griglia media: `rejilla` (1 col), `rejilla dos`, `rejilla tres` (1 colonna su mobile, 2/3 da 900px).
- Video, sempre così (niente autoplay):
  ```html
  <figure class="media">
    <video controls playsinline preload="metadata" poster="poster/minXX.jpg">
      <source src="video/minXX.mp4" type="video/mp4">
    </video>
    <figcaption><span class="min">VÍDEO · MIN XX</span>Nota</figcaption>
  </figure>
  ```
- Immagine: `<a href="img/minXX.jpg"><img loading="lazy" src="img/minXX.jpg" alt="..."></a>`.
- Colori: blu `#0A2B52`, giallo `#FFD84D`, testo `#1A2230`, sfondo `#F4F6F9`.

## Template

`plantillas/informe/index.html` usa percorsi già calcolati per la posizione finale
(4 livelli sotto la root). Nella cartella `plantillas/` i link non risolvono: è voluto.
Il controllo dei link esclude `plantillas/`.

## Verifica

`python -m http.server 8000`, controllare che tutti gli `href`/`src` esistano (escluso `plantillas/`),
layout a 375px e 1280px, video con controlli nativi e schermo intero.
