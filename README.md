# CL-trad

Progetto con le 11 skill di day trading di
[Jakeschincariol/day-trader-skill](https://github.com/Jakeschincariol/day-trader-skill)
(v2.0.0, commit `3d0f4ef`, licenza MIT: vedi `.claude/skills/LICENSE-day-trader-skill`),
installate in `.claude/skills/`. Aprendo questo progetto con Claude Code le skill sono
disponibili come comandi `/trader-…`.

## Le skill

| Comando | A cosa serve |
| --- | --- |
| `/trader-scanner` | Cerca setup (rotture del range d'apertura, flag, rimbalzi) su ~5.900 titoli USA |
| `/trader-news` | Notizie e comunicazioni 8-K SEC sui titoli che segui |
| `/trader-entry` | Segue il setup barra per barra e dice quando entrare |
| `/trader-exit` | Fissa stop e target prima di entrare |
| `/trader-timemachine` | Rigioca la sessione 10.000 volte e sui giorni passati: probabilità realistiche |
| `/trader-budget` | Dimensiona la posizione sul budget e sulla perdita massima per trade |
| `/trader-risk` | Controlla ogni ordine contro i tuoi limiti: PASS o BLOCK |
| `/trader-broker` | Invia l'ordine al broker (paper trading di default), solo dopo il tuo "sì" |
| `/trader-alerts` | Avvisi su prezzo, stop, target e chiusura |
| `/trader-analyst` | Riassume le trimestrali (SEC EDGAR) |
| `/trader-pelosi` | Legge le dichiarazioni di trading dei membri del Congresso USA |

Flusso di un trade: scanner → news → entry → exit → timemachine → budget → risk → broker,
poi alerts mentre la posizione è aperta. Tutto viene salvato in `trader/` (escluso da git).

## Configurazione

- Python 3.8+, nessuna dipendenza da installare.
- Per le skill che usano la SEC (`trader-news`, `trader-analyst`) imposta un'identificazione,
  ad esempio `export SEC_USER_AGENT="Nome Cognome tua@email"`, oppure
  `"sec_user_agent"` in `trader/config.json`.
- Limiti di rischio e budget: copia `.claude/skills/trader-budget/config.example.json`
  in `trader/config.json` e modificalo.
- Broker: `trader-broker` usa il server MCP di Alpaca (account paper);
  esempio in `.claude/skills/trader-broker/claude_desktop_config.example.json`.

## Test

```bash
python3 -m unittest discover -s tests
```

I test girano offline su dati reali salvati in `tests/fixtures/`.

## Limiti

Solo mercato USA; quotazioni Yahoo gratuite, ritardate e non ufficiali. Non è consulenza
finanziaria: nessun ordine parte senza la tua conferma esplicita.
