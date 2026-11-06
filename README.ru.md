# dsh-pet — русская версия (форк)

[English / 中文 README](README.md) · [Upstream PC2005-cloud/dsh-pet](https://github.com/PC2005-cloud/dsh-pet)

**Этот репозиторий** — форк [PC2005-cloud/dsh-pet](https://github.com/PC2005-cloud/dsh-pet) с **полной русификацией**, когда язык DeepSeek Harness — **`ru`**. Отдельного «русского питомца» в конфиге нет: переключение идёт вместе с языком хоста.

Upstream сейчас **не принимает** такой объём (меню на рабочем столе, лоток, пузыри с баланса и т.д.) — только страницы внутри DSH. Здесь мы **развиваем русский опыт сами**; общие исправления по возможности уходят в upstream отдельными маленькими PR.

## Что по-русски при `ru`

- Меню питомца (в том числе **на рабочем столе**), чат, пузыри, панель дел, уведомления, пункт выхода в лотке, автономная страница настроек.
- Тексты **баланса** в пузыре (лимиты, сброс, ошибки).
- Ответы модели в чате и «бормотании» — с русской персоной (если не меняли `whisperPrompt`), подсказками и ослаблением старой китайской истории в контексте.
- Кадры **со словами** — варианты в `dsh-pet/assets/memes/ru/` и `dsh-pet/assets/webm/ru/`.
- Голосовой ввод в чате — распознавание с языком `ru`.

При любом другом языке хоста интерфейс остаётся **как в upstream (китайский chrome)**. Своие тексты в конфиге (имя, персона, мемы) **не переводятся**.

## Что нужно

1. [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) с русским языком интерфейса (например пакет **`@goodandready/dsh-russian-lang`** в профиле).
2. Node **≥ 22.12** — для сборки плагина из исходников.

## Установка из этого форка

Сначала соберите плагин (один раз после каждого `git pull`):

```bash
cd dsh-pet
npm ci
npm run build
```

Подключите **локальную копию** к профилю (путь замените на свой):

```bash
dsh plugin --profile desktop add "file:D:/projects/dsh_pet/dsh-pet"
# или для web-профиля:
dsh plugin --profile web add "file:D:/projects/dsh_pet/dsh-pet"
```

Если `dsh plugin add` пишет «Already up to date», но код менялся — удалите каталог плагина в профиле и добавьте снова:

```powershell
Remove-Item -Recurse -Force "$env:USERPROFILE\.dsh\profiles\desktop\node_modules\dsh-pet"
dsh plugin --profile desktop add "file:D:/projects/dsh_pet/dsh-pet"
```

**Перезапустите DeepSeek Harness.** «Перечитать настройки» в меню питомца **не** подтягивает новый код — только конфиг; после обновления репозитория нужны `npm run build` и переустановка плагина.

Язык хоста кэшируется в `%USERPROFILE%\.dsh\dsh-pet\host-locale.json` — после первого успешного `ru` перезапуск не сбрасывает локаль до загрузки web-клиента.

## Ветки

| Ветка | Содержание |
|--------|------------|
| **`main`** | Русификация + актуальная база upstream (мержим по мере обновлений) |
| `feat/host-locale-ru` | Историческая ветка PR [#301](https://github.com/PC2005-cloud/dsh-pet/pull/301) в upstream |

## Документация upstream

Установка, конфиг, API — как у [оригинала](https://github.com/PC2005-cloud/dsh-pet): [INSTALL.md](INSTALL.md), [CONFIG.md](CONFIG.md), [FEATURES.md](FEATURES.md), [API.md](API.md).

Спецификация поведения локали: [openspec/specs/pet-locale/spec.md](openspec/specs/pet-locale/spec.md).

## Лицензия

Как у upstream: код MIT; ассеты — см. [LICENSE](LICENSE) и README upstream.
