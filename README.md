> **HISTORIALLINEN DOKUMENTTI.** Ajantasainen tila: [docs/STATUS.md](docs/STATUS.md).

# 🏒 Mailajoket Tilastoselain

Streamlit-webappi Mailajokkejen jääkiekon tilastojen selailuun vuosilta 2014-2025.

## Dokumentaatio

| Dokumentti | Sisältö |
|---|---|
| [docs/STATUS.md](docs/STATUS.md) | Ajantasainen tila — tilannetaulukko, mitä seuraavaksi, avoimet päätökset. Luetaan ensin. |
| [docs/CHANGELOG.md](docs/CHANGELOG.md) | Muutoshistoria kuukausittain, uusin ylimpänä, mitä tehtiin ja miksi sillä oli väliä. |
| [CLAUDE.md](CLAUDE.md) | Ylläpito-ohjeet projektissa työskenteleville agenteille/kehittäjille. |
| [DEPLOYMENT.md](DEPLOYMENT.md) | Streamlit Cloud -julkaisuohje. Historiallinen, sisältää vanhentuneita polkuja. |
| [GITHUB_PUSH.md](GITHUB_PUSH.md) | GitHub-remoten lisäysohje. Historiallinen, remote on jo olemassa. |

## Paikallinen asennus

1. **Kloonaa repositorio:**
```bash
git clone <repository_url>
cd MJ_stats
```

2. **Luo virtuaaliympäristö (suositeltavaa):**
```bash
python3.11 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

3. **Asenna riippuvuudet:**
```bash
pip install -r requirements.txt
```

4. **Käynnistä sovellus:**
```bash
streamlit run app.py
```

Sovellus avautuu automaattisesti selaimessa osoitteessa `http://localhost:8501`.

## Streamlit Cloud -deployment

### Vaatimukset

1. **GitHub-repositorio:**
   - Pusketaan projekti GitHubiin
   - Varmista että `mailajoket_2014_2026_dataworkbook.xlsx` on repositoriossa

2. **Streamlit Cloud:**
   - Mene [share.streamlit.io](https://share.streamlit.io)
   - Kirjaudu sisään GitHub-tililläsi
   - Valitse "New app"
   - Valitse repositorio ja haara (yleensä `main` tai `master`)
   - Määritä:
     - **Main file path:** `app.py`
     - **Python version:** 3.11
   - Klikkaa "Deploy!"

### Tiedostorakenne

```
MJ_stats/
├── app.py                              # Pääsovellus
├── requirements.txt                    # Python-riippuvuudet
├── README.md                           # Tämä tiedosto
├── .gitignore                          # Git-ignorointi
├── .streamlit/
│   └── config.toml                     # Streamlit-asetukset
├── mailajoket_2014_2026_dataworkbook.xlsx  # Excel-data
└── src/
    ├── __init__.py
    ├── io.py                           # Excel-datan luku ja validointi
    ├── model.py                        # Datan rikastus ja metriikkafunktiot
    └── ui.py                           # UI-komponentit
```

## Rakenne

- `app.py` - Pääsovellus ja reititys
- `src/io.py` - Excel-datan luku, validointi ja cache
- `src/model.py` - Datan rikastus, joinit ja metriikkafunktiot
- `src/ui.py` - Streamlit UI-komponentit ja välilehdet

## Ominaisuudet

- **Suodattimet:** kausi, vastustaja, koti/vieras
- **Yhteenveto:** perusmetriikat, vastustajat, kumulatiiviset trendit
- **Ottelut:** suodatettu ottelulista CSV-latauksella, kausittainen ottelukalenteri
- **Sarjataulukot:** standings-taulukot kilpailuittain ja kausittain
- **Pelaajat:** pelaajatilastot, leaderboard, kausittaiset trendit
- **Rosterit:** kauden rosterit rooleittain, pelaajien määrät

## Teknologiat

- **Streamlit** - Web-sovelluskehys
- **Pandas** - Datan käsittely
- **Plotly** - Interaktiiviset kuvaajat
- **Openpyxl** - Excel-tiedostojen käsittely

## Lisenssi

Tämä projekti on yksityinen Mailajoket-joukkueen käyttöön.

