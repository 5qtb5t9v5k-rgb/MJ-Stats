# MJ Stats — nykytila

**Päivitetty: 11.4.2026** · Tämä on nykytilan yksi totuuslähde.
Ristiriitatilanteessa tämä voittaa muut dokumentit.

## Missä mennään

| Alue | Tila | Huomio |
|---|---|---|
| Ydintoiminnallisuus (5 välilehteä) | ✅ | Yhteenveto, Ottelut, Sarjataulukot, Pelaajat, Rosterit — toimivat, testattu paikallisesti |
| Data 2014–2025 | ✅ | 156 ottelua kausilta 2014–2015…2024–2025 |
| Data kausi 2015–2016 | ❌ | Seasons-rivi olemassa, ei yhtään ottelua Matches-taulussa |
| Data kausi 2025–2026 | 🟡 | 14 ottelua lisätty 11.4.2026; finaalin tulos puuttuu, Standings-taulukkoa ei ole |
| Datan ylläpitoprosessi | 🟡 | Täysin käsivarainen kopiointi ulkopuolisesta järjestelmästä, ei validointia syötössä |
| Julkaisu / deployment | 🟡 | Ohjeet olemassa (Streamlit Cloud), mutta ei selvinnyt onko sovellus tällä hetkellä oikeasti ajossa |
| CI/CD | ❌ | Ei GitHub Actions -workflowa, ei automaattitestejä, ei linttiä |
| Testit | ❌ | Koodikannassa ei ole yhtään testitiedostoa |
| Secrets / ympäristömuuttujat | ✅ | Ei käytössä yhtään; koko koodikanta tarkistettu, ei os.environ- eikä st.secrets-kutsuja |
| Dokumentaatio | 🟡 | README/DEPLOYMENT/GITHUB_PUSH osittain vanhentuneita, merkitty historiallisiksi |

## Seuraavaksi

1. Täytä finaalin (11.4.2026, Mailajoket–NahU, match_id 170) tulos Matches-välilehdelle kun ottelu on pelattu.
2. Päätä rakennetaanko Standings-taulukko kaudelle 2025–2026, ja jos, millä säännöllä.
3. Päätä korjataanko aiemmin raportoidut UI-bugit ja missä järjestyksessä.

**Odottaa ulkopuolista:** finaalin lopputulos (Mailajoket–NahU, 11.4.2026) — ottelu oli kesken tätä dokumenttia kirjoitettaessa.
**Voi tehdä odottaessa:** Standings-taulukon rakentamistavasta päättäminen, aiemmin raportoitujen UI-bugien korjaaminen, päätös PR:n avaamisesta ja deployment-tilanteen varmistaminen.

## Avoimet päätökset

*Nämä estävät etenemisen ja vaativat ihmisen päätöksen. Lue tämä ensin
kun palaat tauolta.*

| Kysymys | Vaihtoehdot | Mitä odottaa |
|---|---|---|
| Rakennetaanko Standings kaudelle 2025–2026 koodilla Matches-datasta, vai syötetäänkö se käsin ulkopuolisesta lähteestä kuten aiemmat kaudet? | Generointi koodilla / Käsin syöttö | Omistajan päätös + tasapistesäännön valinta jos koodilla |
| Korjataanko aiemmin raportoidut UI-bugit (0–0-tuloksen virheellinen "N/A", roolien luokittelun epäjohdonmukaisuus, pistekeskiarvon laskentavirhe per-kausi-näkymässä)? | Korjataan nyt / Jätetään myöhemmäksi | Omistajan priorisointi |
| Avataanko pull request branchilta `claude/review-mj-stats-ViD7R` `main`-branchiin? | Avataan PR / Jatketaan branchilla | Omistajan päätös |
| Onko sovellus tällä hetkellä julkaistuna ja ajossa Streamlit Cloudissa? | Kyllä, ajossa / Ei, tarvitsee (uudelleen)julkaisun | Ei selvinnyt tästä repositoriosta — vaatii tarkistuksen Streamlit Cloud -tililtä |

## Dokumenttikartta

| Mitä tarvitset | Mistä löytyy |
|---|---|
| Mikä tämä on, miten ajetaan (huom: kausikattavuus vanhentunut) | `README.md` |
| Mitä tapahtui ja miksi | `docs/CHANGELOG.md` |
| Ylläpitosäännöt tälle projektille työskenteleville | `CLAUDE.md` |
| Streamlit Cloud -julkaisuohje (vanhentunut, henkilökohtaisia polkuja) | `DEPLOYMENT.md` |
| GitHub-remoten lisäysohje (vanhentunut, remote on jo olemassa) | `GITHUB_PUSH.md` |

Ei `docs/INFRA.md`:tä — projektilla ei ole ulkoisia palveluita, ympäristömuuttujia
eikä kuluja joita dokumentoida. Luodaan vasta jos näitä tulee.
