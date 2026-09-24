# TODO

Residuals after QA round 2 (word sample seed 31, sentence sample seed 32).
See `tools/REPORT.md` for the rules already in place.

## Words
- Predicatives (нужно, надо, можно, нельзя, жаль) ship as adverbs. A
  "predicative" POS would need an engine-side label; the gloss carries the
  meaning for now.
- есть has one entry, "to eat". Its "is / there is" use (У меня есть...)
  links to быть, which is right, but learners never see есть = "there is"
  as a word of its own.
- ё/е ambiguity inside verb forms: узнаем (pf. future of узнать) and узнаём
  (impf. present of узнавать) fold together, and the tagger picks one.
- Sense order for some B1 homonyms may still lead with a rare sense. All
  A1+A2 glosses were hand-skimmed in round 2; B1 was only sampled.
- Comparatives tagged ADJ (выше, быстрее) link to the adjective or the -о
  adverb depending on the tag. Both are defensible; neither is taught as
  a separate form.
- Hyphenated compound nouns (штаб-квартира) are split by spaCy unless the
  whole word is a Wiktionary headword that also reaches the frequency list.

- A1 sentence difficulty: about 15% of A1 example sentences go beyond A1
  grammar, mostly бы/будь conditionals and subordinate clauses. The A1
  ranker penalises participles, который, oblique cases and rare words, but
  not conditionals.
- убить and убийство sit at A1 by subtitle frequency. Their example
  sentences are kept to B1 by the violence filter; the words stay.
- Minor losses from the v2 reselection (not in the pack any more):
  далёкий, поздний, редко, бесплатный, запад.
- Audio coverage is 33.6% of sentences (v1 34.6%). The bare-form example
  rule adds sentences without audio; a Tatoeba audio request list would
  help.

## Sentence links
- что in "что это за ..." / "Что за ..." and in "что ты хочешь ..." is
  sometimes tagged as the conjunction instead of the pronoun.
- "ни" flips: "ни о чём" and "Сколько ни ..." are sometimes tagged CCONJ
  instead of the particle (both link to ни, the POS entry differs).
- Set phrases: "с тех пор" links пора ("it is time"); a phrase entry would
  be better.
- Some sentences with fewer than 4 tokens still appear at A1 (3 of 812),
  through the shared fallback for A1 words with fewer than 2 candidates.

## Engine / publishing
- vocab-engine must be committed with langs/ru.py and the new hooks before
  `./check.sh` passes without `PACKBUILDER_PATH=../vocab-engine/tools`.
  Then run `git submodule update --remote engine` and rebuild.
- Browser verification is still to do: ru-RU TTS voice, typing without ё or
  stress, the pron toggle showing stress marks, and audio playback.
