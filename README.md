# mVocalToolkit catalog

**English** · [Русский](#русский)

The list of models that [mVocalToolkit](https://github.com/Megageorgio/mVocalToolkit) (and mLabeler through it)
offers: aligners (SOFA, HubertFA, TIFA), phoneme recognisers (WFL-ASR, MCFL), Whisper, GAME, separation, pitch,
vocoders, refiners. Each model is downloaded from where its author published it the first time it is used.

The toolkit reads `catalog.json` from this repository at every start and on every update check, so a model added
here shows up without a new toolkit. Offline it uses the last copy it read, else the copy inside the toolkit.

## Adding a model

Add an entry to `models` in `catalog.json`:

```json
{
  "id": "sofa-xx-mymodel-1.0",
  "engine": "sofa",
  "name": "Language SOFA mymodel 1.0",
  "author": "Who made it",
  "languages": ["xx"],
  "homepage": "https://...",
  "size_hint": "100 MB",
  "source": {"type": "github_release", "repo": "me/models", "tag": "v1", "asset": "mymodel.zip"}
}
```

- `id`: unique and never changed (installed models are found by it).
- `name` without the author: the author goes into `author` and is shown next to the name.
- `engine`: `sofa`, `hubertfa`, `tifa`, `whisperx`, `wfl_asr`, `mcfl`, `game`, `tempo`, `pitch`, `separation`,
  `vocoder`, `refiner`. A toolkit that doesn't have an engine yet doesn't show its models.
- Sources: `url`, `github_release`, `huggingface`, `engine`; packs (one archive with several models) are described in
  the toolkit's [docs/API.md](https://github.com/Megageorgio/mVocalToolkit/blob/main/docs/API.md#catalog-format).
- `format` at the top is the version of the file format. A toolkit older than the format keeps its last copy.

## Adding a dataset

Public singing datasets for training go into `datasets` (format in the toolkit's
[docs/API.md](https://github.com/Megageorgio/mVocalToolkit/blob/main/docs/API.md#datasets)). Every dataset needs its
`license`: name, link, a short summary and what it allows (`training`, `publish_models`, `commercial`,
`redistribution`, `attribution`). A dataset whose license doesn't allow training is not added (the toolkit would hide
it anyway). When the license is unclear, leave the dataset out.

Check that the file is valid JSON before committing: `python -m json.tool catalog.json > /dev/null`.

## Русский

Список моделей, которые предлагает [mVocalToolkit](https://github.com/Megageorgio/mVocalToolkit) (и через него
mLabeler). Тулкит читает `catalog.json` из этого репозитория при каждом запуске и при каждой проверке обновлений:
модель, добавленная сюда, появляется у всех без нового тулкита. В `datasets` — публичные певческие датасеты для
обучения, у каждого обязательно указана лицензия; датасеты, которые нельзя использовать для обучения, не добавляются. Без сети используется последняя прочитанная копия,
а если её нет — копия внутри тулкита.

Чтобы добавить модель, допишите запись в `models` (пример выше). Автора пишите в `author`, а не в название: он
показывается рядом с названием. `id` не меняйте — по нему находятся установленные модели. Модели движков, которых в
тулките ещё нет, старые версии просто не показывают.
