# 🎵 Spotify Dataanalyse: Fra API-udtræk til Statistisk Lydanalyse

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)
![Python](https://img.shields.io/badge/Python-3.13-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-blueviolet)
![Spotify API](https://img.shields.io/badge/Spotify-Web%20API-1DB954)

Dette projekt dokumenterer en komplet dataanalyseproces: Fra opsætning af en Spotify Developer App og håndtering af OAuth2-autentifikation over fejlfinding af API-begrænsninger til en dybdegående statistisk analyse af over 30.000 sange for at afdække, hvad der driver streaming-succes.

---

## 🧭 Projektets To Faser

Projektet er opdelt i to hoveddele, der afspejler den reelle udviklingsproces:
1. **Fase 1: API-integration og teknisk debugging** – Opsætning af live pipeline mod Spotifys Web API.
2. **Fase 2: Explorativ dataanalyse (EDA)** – Statistisk analyse af lydfeatures på et åbent benchmark-datasæt.

---

## 🛠️ Fase 1: Spotify Web API & Fejlfinding i Virkeligheden

Målet var oprindeligt at trække friske data direkte fra Spotifys API via Python-biblioteket `spotipy`. Undervejs stødte projektet på en række reelle API-udfordringer, som blev diagnosticeret og løst:

### 1. Autentifikation og Cloud-miljø (OAuth2 i Colab)
* **Udfordring:** Da Google Colab kører i en cloud-container uden lokal browser, fejlede traditionelle omdirigeringer (`localhost`).
* **Løsning:** Implementering af et headless OAuth-flow (`open_browser=False`) og konfiguration af en sikker callback-URI (`https://example.com/callback`) i Spotify Developer Dashboard.

### 2. Spotifys Endpoint-restriktioner
* **401 Unauthorized på playlister:** Spotifys officielle redaktionelle playlister (`37i9dQ...`) kræver nu brugertoken frem for standard app-credentials.
* **404 Resource Not Found:** Spotify lukkede for direkte udtræk af platformens egne hitlister (Top 50 - Global m.fl.).
* **400 Invalid Limit:** Spotifys API tillader i udviklertilstand ikke opslag på 25–50 tracks ad gangen via søgning; grænsen måtte begrænses til 10 tracks pr. request kombineret med paginafbræk (`offset`).
* **403 Forbidden på `/v1/tracks` og `/v1/audio-features`:** Da Spotify for nylig lukkede adgangen til rå lydparametre for uafhængige udviklere, blev projektet bevidst omlagt til et verificeret historisk datasæt for at kunne gennemføre analysen.

---

## 📊 Fase 2: Explorativ Dataanalyse (EDA)

For at besvare spørgsmålet *"Hvad skaber et hit?"* blev analysen flyttet til **TidyTuesday Spotify-datasættet** med over 30.000 sange med samtlige Spotifys oprindelige lydfeatures.

### 1. Datarensning & Miljøtilpasning
* Fjernelse af dubletter og manglende observationer i nøglefelter (`track_popularity`, `track_name`).
* Konvertering af `duration_ms` til minutter samt bortfiltrering af ekstreme outliers (sange under 1 min eller over 8 min).
* Fejlretning af kompatibilitetsproblemer mellem Seaborn og Python 3.13 (håndtering af `boxprops`-fejl ved at skifte til native Matplotlib-søjlediagrammer).

---

## 📈 Vigtigste Analyseresultater

### Graf 1: Gennemsnitlig popularitet pr. genre
* **Pop** (~48) og **Latin** (~47) opnår den højeste gennemsnitlige lytterscore.
* **EDM** ligger lavest (~35), hvilket skyldes en tung "hale" af niche-remix og klubtracks med meget få streams.

### Graf 2: Korrelationsmatrix (Heatmap)
* **Myten om hit-formlen:** Der er stort set **ingen lineær korrelation** mellem sangens lydmæssige glæde (*valence*, $r = 0{,}03$) eller dansabilitet (*danceability*, $r = 0{,}07$) og dens popularitet.
* **Kortere sange:** Varighed har en svag negativ korrelation med popularitet ($r = -0{,}14$), hvilket stemmer overens med streamingplatformenes incitament til at belønne kortere spilletid.
* **Lydmiks:** Høj energi hænger stærkt sammen med lydstyrke (*energy* vs. *loudness*, $r = 0{,}68$).

### Graf 3: Akustisk fingeraftryk (EDM vs. R&B)
* **EDM:** Koncentreret næsten udelukkende i et snævert interval med meget høj energi ($0{,}60$–$1{,}00$), uanset om sangens stemning er melankolsk eller glad.
* **R&B:** Udviser en bred spredning i både intensitet ($0{,}20$–$0{,}80$) og stemning.

---

## 💡 Forretningsmæssig Konklusion

Analysen demonstrerer grænserne for rent teknisk produktanalyse i kreative industrier:
1. **Lyddata er ikke nok:** Et musikselskab kan ikke modellere sig frem til et hit udelukkende via tempo, dansabilitet eller toneart.
2. **Distribution trumfer komposition:** Kommerciel succes på streamingtjenester afgøres primært af eksterne faktorer som playliste-placering, marketingbudgetter, TikTok-viraliet og kunstnerens brand.

---

## 💻 Tech Stack

* **Sprog & Miljø:** Python 3.13, Google Colab
* **Datahåndtering:** `pandas`, `numpy`
* **Visualisering:** `matplotlib`, `seaborn`
* **API & Protokoller:** `spotipy`, OAuth 2.0 (Authorization Code Flow)

---

## 📂 Filstruktur

```text
├── spotify_analysis.ipynb   # Komplet Google Colab notebook med kode, API-kald og grafer
├── spotify_analysis.png     # Visualisering af de 3 del-analyser
└── README.md                # Projektdokumentation og konklusioner
