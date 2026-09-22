# 🎵 Spotify Hit-Analyse: Hvad skaber et streaming-hit?

En explorativ dataanalyse (EDA) af over 30.000 sange fra Spotify, der undersøger sammenhængen mellem sangenes tekniske lydattributter (BPM, energi, dansabilitet m.fl.) og deres popularitet.

---

## 📌 Projektets formål & hypoteser

Projektet undersøger den klassiske antagelse inden for musikindustrien: *Findes der en teknisk opskrift på et hit?*

**Centrale hypoteser:**
1. Sange med høj *danceability* og høj *energy* opnår systematisk højere popularitetsscore.
2. Der findes en lineær sammenhæng mellem sangens musikalske positivitet (*valence*) og dens lytterappel.
3. Forskellige musikgenrer udviser markante forskelle i popularitetsdistribution og dynamisk spændvidde.

---

## 📊 Vigtigste indsigter

1. **"Hit-formlen" eksisterer ikke i rå lyddata:**
   * Korrelationsanalysen viser, at hverken *danceability* ($r = 0{,}07$) eller *valence* ($r = 0{,}03$) har en statistisk signifikant lineær sammenhæng med popularitetsscoren.
   * Sangens popularitet drives i langt højere grad af eksterne faktorer som kunstnerens etablerede brand, marketingbudgetter og placering på kuraterede playlister end af lydens tekniske opbygning.

2. **Kortere sange har en svag fordel:**
   * Sangens varighed (*duration_min*) har den stærkeste negative korrelation med popularitet ($r = -0{,}14$). Dette stemmer overens med streamingøkonomiens incitamentsstruktur, hvor kortere sange giver højere afspilningsfrekvens og tilpasser sig faldende opmærksomhedsspænd.

3. **Genrernes popularitetsfordeling:**
   * **Pop** og **Latin** opnår det højeste gennemsnitlige popularitetsniveau (~47–48 point), drevet af massiv playliste-eksponering.
   * **EDM** har den laveste gennemsnitlige score (~35 point), hvilket primært skyldes en markant "lang hale" af niche-remix og klubudgivelser med lavt lyttervolumen.

4. **Akustisk fingeraftryk (EDM vs. R&B):**
   * EDM-tracks er næsten universelt begrænset til et snævert højenergi-interval ($0{,}60$–$1{,}00$ i *energy*), uanset om stemningen er melankolsk eller euforisk.
   * R&B udviser betydeligt større dynamisk spændvidde og fordeler sig jævnt over hele energiskalaen.

---

## 🛠️ Tech Stack & Værktøjer

* **Programmeringssprog:** Python 3.10+
* **Datahåndtering:** `pandas`, `numpy`
* **Visualisering:** `matplotlib`, `seaborn`
* **Udviklingsmiljø:** Google Colab / Jupyter Notebook
* **API-erfaring:** Spotify Web API (`spotipy` biblioteket til OAuth-autentifikation og metadataudtræk)

---

## 📁 Datakilde

Analysen tager udgangspunkt i **TidyTuesday Spotify Dataset**, som rummer over 32.000 sange med officielle audio metrics leveret via Spotifys API:
* `track_popularity`: Lytterpopularitet målt fra 0 til 100
* `danceability`, `energy`, `loudness`, `valence`, `tempo`: Spotifys normaliserede lydfeatures
* `playlist_genre`: Kategoriopdeling (pop, rap, rock, r&b, edm, latin)

---

## 🚀 Sådan køres projektet lokalt

1. Klon repositoriet:
   ```bash
   git clone [https://github.com/DIT-BRUGERNAVN/spotify-data-analysis.git](https://github.com/DIT-BRUGERNAVN/spotify-data-analysis.git)
   cd spotify-data-analysis
