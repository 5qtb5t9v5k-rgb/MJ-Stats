# Muutoshistoria

Vain lisätään, uusin alimmaksi. Virheellistä merkintää ei muokata —
korjaus kirjataan uutena merkintänä.

## 2026-01

- **4.1. — Projekti perustettiin.** Ensimmäinen commit toi Streamlit-sovelluksen
  perusrungon (`app.py`, `src/io.py`, `src/model.py`, `src/ui.py`) ja
  Excel-datan vuosilta 2014–2025. Koko rakenne pystytettiin yhden istunnon
  aikana, ei viikkojen projektina.
- **4.1. — Julkaisuputki dokumentoitiin käsivaraiseksi.** `DEPLOYMENT.md`,
  `GITHUB_PUSH.md` ja `push_to_github.sh` lisättiin kuvaamaan manuaalista
  git push + Streamlit Cloud -reittiä. Automaatiota (CI/CD) ei rakennettu —
  tietoinen valinta pienelle sisäiselle työkalulle.
- **4.1. — Tumma teema ja devcontainer lisättiin.** `.streamlit/config.toml`
  sai tumman värimaailman ja `.devcontainer/devcontainer.json` toi GitHub
  Codespaces -tuen (Python 3.11 -pohjainen kontti).
- **4.1. — Logon sijoittelu käännettiin kesken päivän: suunnanmuutos.**
  Logo yritettiin ensin lukita paikalleen sivua vieritettäessä (ensin CSS:llä,
  sitten JavaScriptillä kun CSS ei riittänyt). Päätös kumottiin kokonaan
  saman päivän aikana ja logo tehtiin sen sijaan vierimään sisällön mukana.
  Loppupäivä kului sijainnin ja koon hienosäätöön erikseen työpöytä- ja
  mobiilinäkymille.
- **4.1. — Pieniä UX-siistimisiä.** Infopainike tehtiin auki/kiinni
  -taitettavaksi ja pelaajat-välilehdeltä poistettiin vahingossa jäänyt
  logon duplikaatti.

## 2026-04

- **11.4. — Kausi 2025–2026 syötettiin käsin ulkopuolisesta
  otteluseurannasta.** Käyttäjä toimitti otteludatan kopioi-liitä-muodossa.
  Tästä lisättiin 12 runkosarjaottelua, välierä (voitto VesKiä vastaan
  lisäajalla) ja finaali. Kolme uutta vastustajajoukkuetta (Paperilla
  Parempi, Hot Wings, Tabula Rasa) ja kaksi uutta kilpailua lisättiin
  samalla. Finaalin tulos jätettiin tyhjäksi, koska ottelu oli kesken
  syöttöhetkellä — data odottaa edelleen tätä ulkoista tapahtumaa.
- **11.4. — Löydös kumosi aiemman oletuksen tulosten laskennasta.**
  Finaalin tyhjä tulos paljasti bugin `src/model.py:enrich_matches`-funktiossa:
  koodi oletti maalilukemien olevan aina läsnä kun molemmat joukkueet on
  tiedossa, ja tulkitsi puuttuvat maalit (NaN) tasapeliksi, koska
  `NaN > NaN` palauttaa aina `False`. Pelaamaton ottelu sai näin
  virheellisesti yhden pisteen. Korjattu käsittelemään puuttuvat maalit
  pelaamattomana otteluna kaikissa laskennoissa (outcome, goals_for,
  goals_against, points_from_match).
- **11.4. — Minimidokumentaatio luotu.** `docs/STATUS.md` ja
  `docs/CHANGELOG.md` kirjoitettiin, vanhat ohjedokumentit (`README.md`,
  `DEPLOYMENT.md`, `GITHUB_PUSH.md`) merkittiin historiallisiksi, ja
  `CLAUDE.md` sai ylläpitosäännön joka pitää nämä dokumentit ajan tasalla
  jatkossa ilman erillistä pyyntöä.
