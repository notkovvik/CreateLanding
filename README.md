# CreateLanding

[🇷🇺 Русский](#русский) · [🇬🇧 English](#english)

🔗 **Live demo · Живая версия:** https://notkovvik.github.io/

---

<a id="русский"></a>
## 🇷🇺 Русский

Генератор персональных сайтов на GitHub Pages для витрины ваших репозиториев.

### Что это

Одностраничный конструктор, который собирает статический сайт-каталог ваших репозиториев GitHub. Вводите логин, настраиваете опции, скачиваете `index.html`, кладёте в репозиторий `<логин>.github.io` — сайт работает.

Никакого бэкенда, сборки и зависимостей. Всё происходит в браузере.

### Возможности

Готовый сайт показывает:

- карточки всех публичных репозиториев с описанием, языком и звёздами;
- ссылку на сайт проекта (GitHub Pages или homepage);
- кнопку скачивания исходников в ZIP;
- список файлов последнего релиза;
- поиск и сортировку;
- статистику: количество проектов, звёзд, языков;
- панель диагностики с полем для персонального токена GitHub.

Сам генератор:

- 🔑 Ввод любого логина GitHub
- 🎨 Настройка оформления и сезонных тем
- 🧩 Включение/отключение блоков: статистика, диагностика, сортировка, «Скачать код», релизы
- ⚙️ Настройка времени кеша API
- 👀 Живое превью прямо в браузере
- 💾 Скачивание готового `index.html` одной кнопкой
- 📋 Копирование кода в буфер обмена
- 🚀 Пошаговая инструкция по развёртыванию на GitHub Pages

### Быстрый старт

**1. Сгенерируйте `index.html`**

1. Откройте генератор.
2. Введите ваш логин GitHub (например, `octocat`).
3. Настройте опции по вкусу.
4. Нажмите **«Скачать index.html»**.

**2. Создайте репозиторий**

Имя репозитория должно быть **`<ваш-логин>.github.io`** — тогда сайт откроется по корневому адресу `https://<ваш-логин>.github.io/`. Для логина `octocat` — репозиторий `octocat.github.io`.

Репозиторий должен быть **публичным**.

**3. Загрузите файл**

1. В пустом репозитории нажмите **creating a new file**.
2. Имя файла: `index.html`.
3. Вставьте содержимое скачанного файла.
4. Нажмите **Commit changes**.

**4. Включите GitHub Pages**

1. **Settings** репозитория → **Pages**.
2. **Source**: `Deploy from a branch`.
3. **Branch**: `main`, папка `/ (root)`.
4. **Save**.

Через 1–3 минуты сайт откроется по `https://<ваш-логин>.github.io/`.

### Опции генератора

| Опция | Что делает |
|---|---|
| **Логин GitHub** | Чей профиль показывать |
| **Название сайта** | Заголовок в hero-секции |
| **Описание** | Подзаголовок под названием |
| **Кеш API** | Сколько минут хранить ответы GitHub в localStorage |
| **Статистика** | Блок с числом проектов, звёзд и языков |
| **Сортировка** | Селект «По обновлению / По дате / По алфавиту» |
| **Кнопка «Скачать код»** | Скачивание ZIP-архива ветки |
| **Кнопка «Файлы релизов»** | Раскрывающийся список ассетов последнего релиза |
| **Панель диагностики** | Блок с полем для токена и отладочной информацией |
| **Хэллоуин-тема** | Автовключение 3.10.2026 — 1.11.2026 |
| **Зимняя тема** | Автовключение 1.12.2026 — 1.02.2027 |
| **Кнопка «Обычный вид»** | Возможность отключить сезонную тему |

### Лимиты GitHub API

Без авторизации GitHub даёт **60 запросов в час на IP**. Один заход на сайт с пагинацией тратит несколько запросов. При активном использовании лимит быстро исчерпывается.

Два способа обойти:

1. **Персональный токен GitHub** — поднимает лимит до **5000 запросов в час**. Токен вводится вручную на готовом сайте (в панели «Диагностика») и хранится только в `localStorage` браузера. Никуда, кроме `api.github.com`, не уходит.
2. **Кеш API** — встроен, снижает количество запросов при повторных заходах. Настраивается в генераторе.

**Как создать токен:**

1. Откройте https://github.com/settings/tokens
2. **Generate new token** → **Fine-grained** (безопаснее) или **Classic** (проще).
3. Fine-grained: **Repository access** → нужные репозитории, **Permissions → Contents → Read-only**.
4. Classic: галочка **`repo`**.
5. Скопируйте токен и вставьте его на готовом сайте в панели «Диагностика».

> ⚠️ **Никогда не вставляйте токен в код сайта.** Он попадёт в исходники и будет виден любому через DevTools. Вводите только через интерфейс.

### Приватные репозитории

Публичный GitHub Pages **не показывает приватные репозитории**:

- API отдаёт их только при наличии токена;
- токен нельзя встроить в статический сайт — он окажется в открытом доступе.

Если нужно видеть приватные проекты:

- **Локально:** откройте `index.html` на компьютере и введите токен — он останется только у вас.
- **Публично:** сделайте серверless-прокси (Cloudflare Worker, Vercel Function). Токен хранится в переменной окружения на сервере, сайт обращается к прокси, а не к GitHub напрямую.

### Структура репозитория

```
.
├── index.html   # сам генератор
└── README.md    # этот файл (RU + EN)
```

### Развёртывание генератора

Если хотите поднять свой экземпляр генератора:

1. Форкните или склонируйте репозиторий.
2. Загрузите `index.html` в репозиторий (можно в тот же `<логин>.github.io`, но тогда он займёт корень).
3. Включите GitHub Pages в **Settings → Pages**.
4. Откройте сайт.

Если генератор живёт в репозитории с другим именем (не `<логин>.github.io`), он откроется по адресу `https://<логин>.github.io/<имя-репозитория>/`.

### Как это работает

1. Пользователь заполняет форму.
2. Генератор собирает строку `index.html` из шаблона с подставленными значениями.
3. Пользователь скачивает файл.
4. GitHub Pages отдаёт этот файл как статику.
5. В браузере посетителя скрипт обращается к `api.github.com` и рисует карточки.

Никакие данные пользователя никуда не отправляются. Всё происходит локально.

### Поддерживаемые языки

Для популярных языков заданы фирменные цвета меток: JavaScript, TypeScript, Python, Go, Rust, C++, Kotlin, Swift, Ruby, PHP и другие. Если язык не в списке — используется нейтральный серый.

### Лицензия

Код можно свободно использовать, форкать и адаптировать под себя.

[⬆ Наверх](#createlanding)

---

<a id="english"></a>
## 🇬🇧 English

Generator of personal GitHub Pages sites that showcase your repositories.

### What it is

A single-page builder that creates a static catalog site for your GitHub repositories. Enter your username, tweak the options, download `index.html`, drop it into a `<username>.github.io` repository — the site is live.

No backend, no build step, no dependencies. Everything happens in the browser.

### Features

The generated site includes:

- cards for every public repository with description, language, and stars;
- a link to the project's site (GitHub Pages or homepage);
- a button to download sources as ZIP;
- a list of files from the latest release;
- search and sorting;
- stats: number of projects, stars, languages;
- a diagnostics panel with a field for a personal GitHub token.

The generator itself:

- 🔑 Enter any GitHub username
- 🎨 Configure the layout and seasonal themes
- 🧩 Toggle blocks: stats, diagnostics, sorting, "Download code", releases
- ⚙️ Set the API cache duration
- 👀 Live preview in the browser
- 💾 Download the finished `index.html` with one click
- 📋 Copy the code to clipboard
- 🚀 Step-by-step deployment guide for GitHub Pages

### Quick start

**1. Generate `index.html`**

1. Open the generator.
2. Enter your GitHub username (for example, `octocat`).
3. Configure the options.
4. Click **Download index.html**.

**2. Create a repository**

The repository name must be **`<your-username>.github.io`** — then the site will open at the root URL `https://<your-username>.github.io/`. For the username `octocat`, the repository is `octocat.github.io`.

The repository must be **public**.

**3. Upload the file**

1. In the empty repository click **creating a new file**.
2. File name: `index.html`.
3. Paste the contents of the downloaded file.
4. Click **Commit changes**.

**4. Enable GitHub Pages**

1. Repository **Settings** → **Pages**.
2. **Source**: `Deploy from a branch`.
3. **Branch**: `main`, folder `/ (root)`.
4. **Save**.

In 1–3 minutes the site opens at `https://<your-username>.github.io/`.

### Generator options

| Option | What it does |
|---|---|
| **GitHub username** | Whose profile to display |
| **Site title** | Heading in the hero section |
| **Description** | Subheading under the title |
| **API cache** | How many minutes to keep GitHub responses in localStorage |
| **Stats** | Block with project count, stars, and languages |
| **Sorting** | Dropdown "By update / By date / Alphabetically" |
| **Download code button** | Download the branch ZIP |
| **Release files button** | Expandable list of the latest release assets |
| **Diagnostics panel** | Block with a token field and debug info |
| **Halloween theme** | Auto-enabled Oct 3 — Nov 1, 2026 |
| **Winter theme** | Auto-enabled Dec 1, 2026 — Feb 1, 2027 |
| **Normal view button** | Toggle off the seasonal theme |

### GitHub API limits

Without authorization GitHub allows **60 requests per hour per IP**. One visit to the site with pagination spends several requests. Under active use the limit runs out fast.

Two ways to work around it:

1. **Personal GitHub token** — raises the limit to **5000 requests per hour**. The token is entered manually on the generated site (in the Diagnostics panel) and stored only in your browser's `localStorage`. It goes nowhere except `api.github.com`.
2. **API cache** — built-in, reduces the request count on repeat visits. Configurable in the generator.

**How to create a token:**

1. Open https://github.com/settings/tokens
2. **Generate new token** → **Fine-grained** (safer) or **Classic** (simpler).
3. Fine-grained: **Repository access** → the repositories you need, **Permissions → Contents → Read-only**.
4. Classic: tick **`repo`**.
5. Copy the token and paste it on the generated site in the Diagnostics panel.

> ⚠️ **Never paste the token into the site's code.** It will end up in the page source and be visible to anyone through DevTools. Enter it only through the UI.

### Private repositories

Public GitHub Pages **does not show private repositories**:

- the API returns them only when a token is present;
- the token cannot be embedded into a static site — it would be exposed.

If you need private projects visible:

- **Locally:** open `index.html` on your computer and enter the token — it stays with you only.
- **Publicly:** set up a serverless proxy (Cloudflare Worker, Vercel Function). The token is kept in a server environment variable, and the site talks to the proxy instead of GitHub.

### Repository structure

```
.
├── index.html   # the generator itself
└── README.md    # this file (RU + EN)
```

### Deploying the generator

If you want to host your own instance:

1. Fork or clone the repository.
2. Upload `index.html` to a repository (you can use `<username>.github.io`, but it will occupy the root).
3. Enable GitHub Pages in **Settings → Pages**.
4. Open the site.

If the generator lives in a repository with another name (not `<username>.github.io`), it opens at `https://<username>.github.io/<repo-name>/`.

### How it works

1. The user fills in the form.
2. The generator assembles the `index.html` string from a template with substituted values.
3. The user downloads the file.
4. GitHub Pages serves it as static content.
5. The visitor's browser calls `api.github.com` and renders the cards.

No user data is sent anywhere. Everything happens locally.

### Supported languages

Popular languages have brand colors on their labels: JavaScript, TypeScript, Python, Go, Rust, C++, Kotlin, Swift, Ruby, PHP, and others. Languages not in the list use a neutral gray.

### License

The code is free to use, fork, and adapt.

[⬆ Back to top](#createlanding)
