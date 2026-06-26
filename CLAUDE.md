# CLAUDE.md — правила проекта Chakipaki

Эти правила обязательны к соблюдению в каждой сессии.

## Контекст инфраструктуры (как сейчас устроен деплой)

- Студия **Chakipaki** — набор отдельных мини-игр. Один TikTok-канал, один домен **chakipaki.com**, но каждая игра — самостоятельное приложение.
- Хостинг: **GitHub Pages** через GitHub Actions (workflow `.github/workflows/pages.yml`, `build_type: workflow`).
- Репозиторий деплоя на этом компьютере: `/Users/john13/drakosha-deploy` (remote `wolllk13/drakosha-dragons`, ветка `main`).
- Домен привязан файлом `CNAME` (`chakipaki.com`). Cloudflare DNS — записи в режиме **DNS only** (серое облачко), без проксирования.
- Обновление сайта: положить файлы в репозиторий деплоя → `git add` → `git commit` → `git push origin main`. Actions сам пересобирает и публикует через ~30–60 c.
- Legacy-сборщик Pages зависал; если деплой «застрял в building» — причина обычно в нём. Использовать только Actions-деплой.

## Правила выпуска игр (обязательно соблюдать перед публикацией ЛЮБОЙ игры)

Это студия Chakipaki — набор отдельных мини-игр. Один TikTok-канал, один домен chakipaki.com, но каждая игра — самостоятельное приложение. ПЕРЕД тем как задеплоить или опубликовать любую новую игру, ОБЯЗАТЕЛЬНО убедись, что у неё есть всё перечисленное, и НЕ публикуй, если чего-то не хватает:

1. **Свой адрес:** каждая игра живёт на своём поддомене (например `dragon.chakipaki.com`, `elephant.chakipaki.com`) или в своей папке (`chakipaki.com/dragon`). Игры не перезаписывают друг друга.
2. **Своё название:** уникальные `<title>` и `<meta name="apple-mobile-web-app-title">` внутри игры (например "Chakipaki — Dragons", "Chakipaki — Elephant").
3. **Своя иконка:** свой `apple-touch-icon` (`icon-180.png`) и свой набор иконок (`icon-192.png`, `icon-512.png`) в папке этой игры, не общие с другими играми.
4. **Свой `manifest.json`** со своими `name`, `short_name`, иконками и `theme_color`, лежащий рядом с `index.html` этой игры.
5. **Хранилище на `localStorage`** (не `window.storage`), с уникальными ключами для каждой игры, чтобы прогресс игр не пересекался.

Если для новой игры не хватает иконки, манифеста, названия или отдельного адреса — **ОСТАНОВИСЬ** и запроси недостающее у пользователя, прежде чем деплоить.

### Чек-лист подключения иконки в `<head>` (без него iOS не покажет иконку)

```html
<link rel="manifest" href="manifest.json">
<link rel="apple-touch-icon" href="icon-180.png">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="Chakipaki — <Имя игры>">
<meta name="theme-color" content="#160f33">
```
