# CLAUDE.md — MJ Stats

Ohjeet tässä projektissa työskenteleville agenteille/kehittäjille.

## Dokumentaation ylläpito

Osana jokaista merkittävää muutosta, ilman erillistä pyyntöä:

- Jos tila muuttui (vaihe valmis, päätös tehty, ulkoinen vastaus saapui):
  päivitä `docs/STATUS.md`. Ylikirjoita vanha teksti, älä kerrosta.
- Jos tapahtui jotain merkittävää: lisää rivi `docs/CHANGELOG.md`:hen —
  päivä, mitä, miksi sillä oli väliä.
- Jos palvelu, ympäristömuuttuja tai kulu muuttui: päivitä `docs/INFRA.md`.
- Jos ajastus (cron/workflow) muuttui: päivitä myös README:n ajastuskuvaus
  samassa commitissa.
- Jos dokumentti ja koodi ovat ristiriidassa: **koodi on totuus** — korjaa
  dokumentti samassa commitissa.
- Jos huomaat dokumentaation väittävän jotain mitä koodi ei tee, kerro
  siitä erikseen — älä korjaa hiljaa kumpaankaan suuntaan.

Älä luo uusia tilannekatsausdokumentteja. Yksi STATUS, yksi CHANGELOG.
