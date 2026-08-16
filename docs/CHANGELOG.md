# Muutosloki

Tämä loki kertoo, mitä projektissa on tehty ja miksi sillä oli väliä — se ei ole
committien luettelo. Ajankohdat perustuvat git-historiaan (`git log`). Ajantasainen
tilannekuva on aina `docs/STATUS.md`:ssä; tämä tiedosto on historiaa.

## Tammikuu 2026

**4.1.2026 — Projekti perustettiin yhden päivän aikana.** Ensimmäinen commit toi
mukanaan koko sovelluksen perusrungon: Streamlit-sovellus (`app.py`), kolme
moduulia (`src/io.py` datan lukuun ja validointiin, `src/model.py` datan
rikastukseen ja metriikoihin, `src/ui.py` viiteen välilehteen) ja
Excel-datatiedosto vuosien 2014–2025 otteluhistorialla. Kaikki myöhemmät
saman päivän commitit rakentuvat tämän päälle — kyseessä oli yhden istunnon
pystytys, ei viikkojen projekti.

**4.1.2026 — Julkaisuputki dokumentoitiin käsivaraiseksi.** `DEPLOYMENT.md`,
`GITHUB_PUSH.md` ja `push_to_github.sh` lisättiin samana päivänä. Ne kuvaavat
manuaalisen reitin: koodi pushataan GitHubiin komentoriviltä tai skriptillä,
minkä jälkeen Streamlit Cloud deployaa sovelluksen `app.py`:stä. Automaatiota
(CI/CD, GitHub Actions) ei rakennettu — tämä oli tietoinen valinta pienelle
sisäiselle työkalulle, ei myöhempi puute.

**4.1.2026 — Tumma teema ja devcontainer.** `.streamlit/config.toml` sai
tumman värimaailman ("Fix dark theme configuration", "Change theme to dark
mode"), ja `.devcontainer/devcontainer.json` lisättiin GitHub Codespaces
-tukea varten (Python 3.11 -pohjainen kontti, joka asentaa
`requirements.txt`:n ja käynnistää Streamlitin automaattisesti portissa 8501).

**4.1.2026 — Logon sijoittelua iteroitiin yli 15 committin verran, ja
suunta vaihtui kesken kaiken.** Logo lisättiin ensin oikeaan yläkulmaan.
Sen jälkeen sitä yritettiin lukita paikalleen sivua vieritettäessä — ensin
CSS:llä ("Ensure logo stays fixed... when scrolling"), sitten
JavaScript-korjauksella, kun CSS ei riittänyt ("Fix logo to stay fixed when
scrolling using JavaScript"). Tämä lähestymistapa hylättiin kokonaan: seuraava
commit kääntää päätöksen ympäri ja tekee logosta sivun mukana vierivän
("Change logo to scroll with page content (not fixed)"). Tämän jälkeen
sijaintia ja kokoa hienosäädettiin erikseen työpöytä- ja
mobiilinäkymille useassa pienessä askeleessa, kunnes päädyttiin nykyiseen
ratkaisuun (base64-upotettu kuva, `mj-logo-container`-CSS, erillinen
mediakysely alle 768px leveille näytöille). Tämä on ainoa selkeä
suunnanmuutos koko historiassa: fixed-positiointi kokeiltiin ja hylättiin
saman päivän aikana.

**4.1.2026 — Pieniä UX-siistimisiä.** Infopainike ("Voit muuttaa
suodattimia...") tehtiin auki/kiinni-taitettavaksi (`st.expander`), ja
pelaajat-välilehdeltä poistettiin sinne vahingossa jäänyt logon duplikaatti.

## Huhtikuu 2026

**11.4.2026 — Kausi 2025–2026 syötettiin käsin ulkopuolisesta
otteluseurantajärjestelmästä.** Käyttäjä toimitti otteludatan
kopioi-liitä-muodossa ("Kaikki ottelut" -listaus, jossa näkyi päivämäärä,
areena, kellonaika ja tulos). Tästä lisättiin Excel-työkirjaan 12
runkosarjaottelua, välierä (24.3.2026, MJ–VesKi 4–3 voitto lisäajalla) ja
finaali (11.4.2026, MJ–NahU). Kolme uutta vastustajajoukkuetta
(Paperilla Parempi, Hot Wings, Tabula Rasa) ja kaksi uutta kilpailua
(P-S Harraste A -runkosarja ja sen playoff) lisättiin samalla. Finaalin
tulos syötettiin tyhjänä, koska ottelu oli dokumentointihetkellä vielä
pelaamatta samana päivänä — tämä on ulkoinen tapahtuma jota data odottaa
edelleen.

**11.4.2026 — Löydös kumosi aiemman oletuksen tulosten laskennasta.**
Finaalin syöttäminen ilman maalilukemia paljasti bugin
`src/model.py:enrich_matches`-funktiossa: koodi oli kirjoitettu olettaen,
että `home_goals`/`away_goals` ovat aina läsnä silloin kun molemmat
joukkueet on tiedossa. Kun tämä ei enää pitänyt paikkaansa (pelaamaton
ottelu, tyhjät maalit), Python vertaili `NaN > NaN`:ia, mikä palautti
`False` sekä voitto- että tappiovertailussa ja laski ottelun
automaattisesti tasapeliksi — yhden pisteen arvoisena, vaikka ottelua ei
ollut pelattu. Korjaus lisäsi eksplisiittisen NaN-tarkistuksen maalien
kentille outcome-, goals_for-, goals_against- ja
points_from_match-laskennassa, jolloin pelaamaton ottelu jää nyt oikein
pois kaikista yhteenvedoista kunnes tulos syötetään.
