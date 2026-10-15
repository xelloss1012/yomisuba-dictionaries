# EReader dictionaries

Optional dictionaries of Japanese words that the EReader app downloads on demand from its settings screen, one per interface language without a bundled dictionary. Spanish and English (JMdict) ship with the app.

| File | Glosses | Entries | Source | License |
|---|---|---|---|---|
| `ja-ja-dictionary.json.gz` | Japanese definitions and synonyms (国語辞典) | 109,370 | [Japanese Wiktionary](https://ja.wiktionary.org/) | CC BY-SA 4.0 |
| `jmdict-de.json.gz` | German | 129,088 | [JMdict/EDICT](https://www.edrdg.org/wiki/JMdict-EDICT_Dictionary_Project.html) © EDRDG | [CC BY-SA 4.0](https://www.edrdg.org/edrdg/licence.html) |
| `jmdict-fr.json.gz` | French | 15,336 | [JMdict/EDICT](https://www.edrdg.org/wiki/JMdict-EDICT_Dictionary_Project.html) © EDRDG | [CC BY-SA 4.0](https://www.edrdg.org/edrdg/licence.html) |
| `wiktionary-zh.json.gz` | Chinese | 75,094 | [Chinese Wiktionary](https://zh.wiktionary.org/) | CC BY-SA 4.0 |
| `wiktionary-ko.json.gz` | Korean | 12,243 | [Korean Wiktionary](https://ko.wiktionary.org/) | CC BY-SA 4.0 |
| `wiktionary-it.json.gz` | Italian | 2,763 | [Italian Wiktionary](https://it.wiktionary.org/) | CC BY-SA 4.0 |
| `wiktionary-vi.json.gz` | Vietnamese | 1,645 | [Vietnamese Wiktionary](https://vi.wiktionary.org/) | CC BY-SA 4.0 |

Each file is an adaptation of its source and is distributed under the same license ([CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)). The Wiktionary files come from the extracts published by [kaikki.org](https://kaikki.org/) (wiktextract); JMdict data from the [EDRDG](https://www.edrdg.org/) release of 2026-10-15.

## Format

A gzip-compressed JSON array of entries:

```json
{ "id": "…", "k": ["spellings"], "r": ["readings"], "s": [{ "p": ["part of speech"], "g": ["glosses"] }], "y": ["synonyms"], "i": 1 }
```

`y` (synonyms) and `i` (the word conjugates) only appear in the Wiktionary files.

## Regenerating

With the scripts of the app repository:

```sh
# JMdict (fre, ger, …)
python scripts/build_jmdict_language.py ger jmdict-de.json.gz

# Wiktionary: any extract of the edition (full raw dump or per-language file)
curl -LO https://kaikki.org/jawiktionary/raw-wiktextract-data.jsonl.gz
node scripts/build-wiktionary-dictionary.mjs raw-wiktextract-data.jsonl.gz ja-ja-dictionary.json.gz
```

After publishing a new file, update its `version`, `approxBytes` and `entries` in `src/utils/optionalDictionaries.ts` so installed copies offer the update.
