# EReader dictionaries

Optional dictionaries that the EReader app downloads on demand from its settings screen.

## `ja-ja-dictionary.json.gz` — Japanese–Japanese dictionary (国語辞典)

- **Content:** about 109,000 Japanese headwords with Japanese definitions, readings, alternative spellings and synonyms.
- **Source:** [Japanese Wiktionary (ウィクショナリー日本語版)](https://ja.wiktionary.org/), from the extract published by [kaikki.org](https://kaikki.org/jawiktionary/) (wiktextract), dump of 2026-10-01.
- **License:** [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). This file is an adaptation of Wiktionary content (Wiktionary contributors) and is distributed under the same license.
- **Format:** gzip-compressed JSON array, one entry per line:
  `{ "id", "k": [spellings], "r": [readings], "s": [{ "p": [part of speech], "g": [definitions] }], "y": [synonyms] }`.

### Regenerating

The file is built by `scripts/build-ja-dictionary.mjs` in the app repository:

```sh
curl -LO https://kaikki.org/jawiktionary/raw-wiktextract-data.jsonl.gz
node scripts/build-ja-dictionary.mjs raw-wiktextract-data.jsonl.gz ja-ja-dictionary.json.gz
```

After publishing a new file, bump `JAPANESE_DICTIONARY_VERSION` in the app so installed copies offer the update.
