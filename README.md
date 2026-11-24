# Paolo · Entrenador de porteros

Sito statico (HTML + un solo CSS, niente build) pubblicato su GitHub Pages.
Pensato per essere aperto dal cellulare dai portieri.

## Struttura delle cartelle

```
/
├── index.html                          Home
├── temporada-2026-27/
│   └── apa-poble-sec/
│       ├── index.html                  Pagina squadra (stagione + elenco informe)
│       └── informes/
│           └── 2026-11-21-cornella/
│               ├── index.html          Informe del portero vs UE Cornellà
│               ├── video/              Clip MP4
│               ├── poster/             Fotogramma iniziale di ogni clip (.jpg)
│               └── img/                Screenshot
├── assets/
│   ├── css/style.css                   Unico CSS condiviso
│   └── img/logos/                      Loghi dei club
├── plantillas/informe/index.html       Template vuoto di informe
├── .nojekyll                           GitHub Pages serve i file così come sono
├── README.md
└── CLAUDE.md                           Convenzioni per Claude Code
```

## Come aggiungere un informe

1. Copiare `plantillas/informe/` in
   `temporada-AAAA-AA/<squadra>/informes/AAAA-MM-GG-<rival>/`
   (es. `temporada-2026-27/apa-poble-sec/informes/2026-11-28-europa/`).
2. Creare dentro `video/`, `poster/`, `img/`:
   - `video/`: clip MP4 H.264, idealmente sotto i 10 MB ciascuna, nome `minXX.mp4`
     (minuto di gioco; se non è un minuto, `clipXX.mp4`).
   - `poster/`: stesso nome in `.jpg`.
   - `img/`: screenshot `minXX.jpg`.
3. Se serve, salvare il logo del rivale in `assets/img/logos/<rival>.png`.
4. Compilare i testi (tutto ciò che è tra parentesi quadre), duplicare o cancellare le schede media.
5. Aggiungere la scheda della partita nella pagina squadra (`Informes de partido`, la più recente in alto).
6. Commit e push:
   ```
   git add .
   git commit -m "Informe vs <rival>"
   git push
   ```

### Convertire una clip Veo e generare il poster

```
ffmpeg -i input.mp4 -vf "scale=-2:720" -c:v libx264 -preset veryfast -crf 26 -pix_fmt yuv420p -movflags +faststart -an video/min06.mp4
ffmpeg -ss 0.5 -i input.mp4 -frames:v 1 -vf scale=1280:-2 -q:v 3 poster/min06.jpg
```

Togliere `-an` se si vuole tenere l'audio. Se i video diventano troppo pesanti, usare `-crf 28`.

## Come aggiungere una nuova stagione o squadra

1. Creare la cartella, es. `temporada-2027-28/<squadra>/index.html`
   (copiando la pagina squadra esistente e sistemando i percorsi relativi `../`).
2. Aggiungere la voce nel **menu di tutte le pagine** (home, pagine squadra, ogni informe, template).
   Il menu è il blocco `<details class="menu">` nell'header.
3. Aggiornare il blocco "Temporada actual" della home se cambia la stagione.

## Provare in locale

```
python -m http.server 8000
```

e aprire `http://localhost:8000`.

## Limiti GitHub Pages

- File singolo massimo 100 MB, sito consigliato sotto 1 GB.
- Il repository è pubblico: tutto, video compresi, è visibile a chi ha il link.
