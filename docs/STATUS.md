# Tilannekatsaus

**Päivitetty: 11.4.2026.** Jos tämä dokumentti on ristiriidassa minkä tahansa
muun tiedoston kanssa (README, DEPLOYMENT, GITHUB_PUSH tai vanhat
tilannekatsaukset), **tämä dokumentti voittaa**. Muut tiedostot voivat olla
vanhentuneita eikä niitä ole systemaattisesti pidetty ajan tasalla.

## Tilanne alueittain

| Alue | Tila | Selitys |
|---|---|---|
| Sovelluksen ydintoiminnallisuus | ✅ | Viisi välilehteä (Yhteenveto, Ottelut, Sarjataulukot, Pelaajat, Rosterit) toimivat ja lukevat Excel-datan `src/io.py`:n kautta. Ajettu paikallisesti onnistuneesti tämän dokumentoinnin yhteydessä. |
| Data — ottelut 2014–2025 | ✅ | 156 ottelua kausilta 2014–2015…2024–2025. |
| Data — kausi 2015–2016 | ❌ | Seasons-taulussa on rivi kaudelle, mutta Matches-taulussa ei ole yhtään ottelua tältä kaudelta. Aukko datassa, ei bugi koodissa. |
| Data — kausi 2025–2026 | 🟡 | 14 ottelua lisätty käsin 11.4.2026: 12 runkosarjaa + välierä (valmis) + finaali (tulos puuttuu, ottelu oli kesken dokumentointihetkellä). Standings-taulukkoa tälle kaudelle ei ole. |
| Datan ylläpitoprosessi | 🟡 | Täysin manuaalinen: joku kopioi ottelutulokset ulkopuolisesta järjestelmästä ja Excel-työkirjaa muokataan käsin (nyt myös skriptillä avustettuna). Ei automaattista syöttöä eikä validointia syötettäessä. |
| Julkaisu / deployment | ❓ | Ohjeet olemassa (Streamlit Cloud, ks. DEPLOYMENT.md), mutta ei selvinnyt onko sovellus tällä hetkellä oikeasti julkaistuna ja ajossa jossain URL:ssa. Ei näkyvyyttä tähän tästä repositoriosta. |
| CI/CD | ❌ | Ei GitHub Actions -workflowa, ei automaattitestejä, ei linttiä ajossa. Julkaisu on täysin käsivarainen (git push + Streamlit Cloud -auto-deploy). |
| Testit | ❌ | Koodikannassa ei ole yhtään testitiedostoa. |
| Secrets / ympäristömuuttujat | ✅ | Sovellus ei käytä yhtään ympäristömuuttujaa eikä `st.secrets`-arvoa (tarkistettu koko koodikannasta). `.gitignore` varautuu `.streamlit/secrets.toml`-tiedostoon, mutta sitä ei ole olemassa eikä tarvita. |
| Dokumentaatio (README/DEPLOYMENT/GITHUB_PUSH) | 🟡 | Osittain vanhentunut — ks. erillinen ristiriitaraportti keskustelussa. Kausikattavuus ("2014-2025") ei enää pidä paikkaansa datan kanssa, ja deployment-ohjeissa on henkilökohtaisia polkuja/nimiä jotka eivät vastaa nykyistä repoa. |

## Mitä seuraavaksi ja mikä odottaa ulkopuolista

- **Odottaa ulkopuolista tapahtumaa:** finaalin (11.4.2026, Mailajoket–NahU,
  match_id 170) tulos. Kun ottelu on pelattu, `home_goals`- ja
  `away_goals`-solut täytetään Excel-työkirjan Matches-välilehdellä samalle
  riville, ja tarvittaessa `ot_note`-sarake ("VL" tai "JA"). Mikään muu
  muutos ei ole tarpeen — kaikki laskennat päivittyvät automaattisesti kun
  luvut on syötetty.
- **Tekemättä, ei vielä aikataulutettu:** kauden 2025–2026 Standings-taulukko.
  Sitä ei ole generoitu eikä syötetty käsin. Ks. avoimet päätökset alla.
- **Tekemättä, ei vielä aikataulutettu:** kauden 2015–2016 ottelujen
  jäljittäminen ja lisääminen, jos data on jostain saatavilla.
- **Tekemättä, ei vielä aikataulutettu:** aiemmin (samassa keskustelussa)
  raportoidut UI/logiikkabugit — ks. avoimet päätökset.

## Avoimet päätökset

Tämä on dokumentin tärkein osio: nämä ovat kohtia joissa työ on pysähtynyt
siihen asti, että joku tekee valinnan. Kukin vaatii ihmisen päätöksen, ei
lisätutkimusta.

1. **Generoidaanko Standings-taulukko kaudelle 2025–2026 Matches-datasta, vai
   jätetäänkö se tyhjäksi kunnes joku syöttää sen käsin ulkopuolisesta
   lähteestä?** Jos generoidaan koodilla, pitää päättää lasketaanko sijoitus
   pisteiden vai maalieron perusteella tasapisteissä — tätä sääntöä ei ole
   dokumentoitu missään. Aiemmissa kausissa Standings on aina tullut
   ulkopuolisesta lähteestä (raw_row-sarake Standings-taulussa viittaa
   alkuperäiseen syöttötapaan), joten kaudelle 2025–2026 pitäisi päättää
   pysytäänkö samassa tavassa vai vaihdetaanko laskentatapaan.

2. **Korjataanko aiemmin tunnistetut UI/logiikkabugit, ja jos, missä
   järjestyksessä?** Nämä on raportoitu käyttäjälle aiemmassa
   keskustelussa mutta ei vielä valittu tehtäväksi: virheellinen 0–0
   tasapelin korvaaminen "N/A"-tekstillä ottelunäkymässä
   (`src/ui.py`, Tulos-sarake), roolien luokittelun epäjohdonmukaisuus
   rostereissa (kovakoodattu suomenkielinen lista vs. substring-matchaus
   kahdessa eri kohdassa), sekä pelaajien pistekeskiarvon laskentavirhe
   per-kausi-näkymässä. Tekninen korjaus on suoraviivainen; avoin kysymys on
   priorisointi ja ajoitus, ei toteutustapa.

3. **Avataanko pull request branchilta `claude/review-mj-stats-ViD7R`
   `main`-branchiin, vai jatketaanko työtä suoraan tällä branchilla?**
   Tähän mennessä kaikki muutokset (kausidata, bugikorjaus, tämä
   dokumentaatio) on pushattu `claude/review-mj-stats-ViD7R`-branchille eikä
   PR:ää ole avattu. `main` on yhä siinä tilassa kuin 4.1.2026.

4. **Julkaistaanko sovellus (uudelleen) Streamlit Cloudiin nyt kun dataa on
   päivitetty, ja jos, kuka omistaa sen deployment-tilin?** Tästä repositoriosta
   ei ole näkyvyyttä siihen onko aiempi deployment yhä ajossa tai
   vanhentunut.

## Dokumenttikartta

- `docs/STATUS.md` — tämä tiedosto. Ajantasainen tilanne, luetaan ensin.
- `docs/CHANGELOG.md` — historia kuukausittain ryhmiteltynä, miksi-selityksin.
- `CLAUDE.md` — ylläpito-ohjeet tälle projektille työskenteleville
  agenteille/kehittäjille, mukaan lukien sääntö näiden dokumenttien
  päivittämisestä.
- `README.md` — **HISTORIALLINEN DOKUMENTTI.** Asennus- ja
  yleiskuvausohje, kirjoitettu 4.1.2026. Kausikattavuus vanhentunut.
- `DEPLOYMENT.md` — **HISTORIALLINEN DOKUMENTTI.** Streamlit Cloud
  -julkaisuohje, sisältää henkilökohtaisia tiedostopolkuja.
- `GITHUB_PUSH.md` — **HISTORIALLINEN DOKUMENTTI.** GitHub-remoten
  lisäysohje, tarpeeton nyt kun remote on jo olemassa ja yhdistetty.
- `push_to_github.sh` — skripti GITHUB_PUSH.md:n ohjeen automatisointiin.
  Ei vanhentunut per se, mutta tarpeeton nykyisessä ympäristössä jossa
  git-integraatio on jo valmiina.
