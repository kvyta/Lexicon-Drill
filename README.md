# Lexicon Drill

A rapid-fire, 5-option multiple-choice SAT/PSAT vocabulary quiz. 496 high-frequency
words are grouped into ~66 fine-grained meaning clusters (e.g. *loquacious / garrulous
/ voluble / effusive* under "talkative"); wrong answers are drawn from a word's own
cluster first, always matching its part of speech, so options can't be eliminated on
grammar and are genuine near-synonyms rather than easy throwaways.

- **Word → Definition** and **Definition → Word** questions, evenly weighted.
- Graded on the spot; each next question is generated only after you answer.
- Missed words are saved to a **Review** bank for a last-week-before-the-test drill.
- Add-to-Home-Screen ready on iOS/Android (`manifest.json`, apple touch icon, safe-area CSS).

## Files

- `index.html` + `words.js` — the app, as published to claude.ai (hosted version:
  progress saved to browser `localStorage`).
- `lexicon-drill.html` — the same app bundled into one self-contained file for local/
  offline or mobile (Add to Home Screen) use. Progress lives in the browser by default
  (`localStorage`); on Chromium desktop browsers you can also "Connect a save file,"
  which keeps a living copy of this *entire HTML file* — app plus your progress baked
  in — in sync on disk via the File System Access API. There's never a separate JSON
  file: reopening that one `.html` file restores everything, and "Import a save file"
  reads progress back out of any such file (e.g. after switching devices).
- `generate_words.py` — builds the word bank: clusters, definitions, and the
  same-cluster/related-cluster distractor pools, output as `words_data.json` → `words.js`.
- `manifest.json`, `icon-*.png` — home-screen install metadata.

## Regenerating the word data

```
python3 generate_words.py   # writes words_data.json
python3 -c "import json; d=json.load(open('words_data.json')); open('words.js','w').write('const WORD_DATA = ' + json.dumps(d, separators=(',',':')) + ';')"
```
