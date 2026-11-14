# Антон Бычковский — AI Video Production · Landing

Одностраничный портфолио-лендинг. Прикрепляется ссылкой к отклику на вакансию или
к разговору в чате. Не собирает контакты, не имеет формы, не является воронкой.

**EN primary · RU switcher в правом верхнем углу**

---

## Структура папки

```
landing/
├── index.html              ← единственный исполняемый файл
├── privacy.html            ← privacy policy
├── README.md               ← вы здесь
└── assets/
    ├── posters/            ← стоп-кадры showcase-роликов (6 JPG, ~270 KB)
    └── prod-posters/       ← стоп-кадры продакшн-блоков (10 JPG, ~1.4 MB)
```

**Размер папки целиком:** ~1.7 MB. Страница — полностью статическая: ни одного
`<video>`, ни одного внешнего embed. Всё, что раньше было автоплеем, теперь
заменено статичными кадрами из тех же роликов.

**Видео лежат вне репозитория** (чтобы не публиковать 272 MB и не грузить их
посетителям):

```
C:\Users\DELL\.minimax\workspace\portfolio-prep\videos-source\
├── prod-videos\   ← 5 mp4 (слои продакшна)
├── showcase\      ← 8 mp4 (портфолио-ролики)
├── blackeye\      ← 25 файлов (Black Eye marketing)
└── _autostills-scratch\ ← автоматически извлечённые кадры (не публикуются)
```

Чтобы вернуть ролик на страницу — достаточно добавить `<video>` и положить mp4
обратно в `assets/`. Для статики достаточно постеров: они уже являются кадрами
из соответствующих видео.

---

## Локальный просмотр (проверить перед заливкой)

GitHub Pages обслуживает статику. На своей машине проще всего поднять одноразовый
сервер на Python и открыть в браузере.

```powershell
cd C:\Users\DELL\.minimax\workspace\portfolio-prep\landing
py -m http.server 8000
# открыть http://localhost:8000
```

> **Важно.** Двойной клик по `index.html` (`file://` протокол) тоже сработает, но
> проверять трафик и вес страницы нужно через localhost — только там видно
> реальные сетевые запросы.

---

## Деплой на GitHub Pages (рекомендуемый путь)

Инструкция — от @jeminai (коллега Антона, проверено 2026-08-19).

### Шаг 1. Аккаунт GitHub

Регистрация бесплатна, ~1 минута: <https://github.com/signup>.

### Шаг 2. Новый репозиторий

1. Плюс `+` в правом верхнем углу → **New repository**.
2. **Repository name** — например `ai-video-pipeline` или `bychkovsky-portfolio`.
3. Галочка **Public** (обязательно для бесплатного хостинга).
4. **Create repository**.

### Шаг 3. Загрузка файлов

1. На открывшейся странице репозитория кликнуть по ссылке
   **uploading an existing file**.
2. Перетащить мышкой всю папку `landing/` (с `index.html` + `assets/`) прямо в окно
   браузера.
3. **Важно:** главная страница должна называться строго `index.html` — не
   `index.htm`, не `main.html`, не в подпапке.
4. Кнопка **Commit changes** внизу страницы.

> **Альтернатива через Git CLI** (если уже настроен):
> ```bash
> cd C:\Users\DELL\.minimax\workspace\portfolio-prep\landing
> git init
> git add .
> git commit -m "Initial portfolio landing"
> git branch -M main
> git remote add origin https://github.com/<your-login>/<repo-name>.git
> git push -u origin main
> ```

### Шаг 4. Включить GitHub Pages

1. В репозитории — вкладка **Settings** (в верхнем меню).
2. В левом меню — раздел **Pages**.
3. Блок **Build and deployment** → поле **Source** → выбрать
   **Deploy from a branch**.
4. Поле ниже (**Branch**) — выбрать `main` (или `master`).
5. Кнопка **Save**.

### Шаг 5. Получить ссылку

Через 1–2 минуты появится надпись *«Your site is live at…»*. Обновить страницу.
Готовая ссылка вида:

```
https://<your-login>.github.io/<repo-name>/
```

Ссылка постоянна, пока репозиторий существует.

---

## Альтернативные хостинги

| Сервис      | Плюсы                                          | Минусы                            |
|-------------|------------------------------------------------|-----------------------------------|
| **Netlify**  | Drag-n-drop папки, custom domain, instant HTTPS | Лимит 100 GB bandwidth / month    |
| **Vercel**   | То же, плюс preview-URL для каждого коммита     | Лимит 100 GB bandwidth / month    |
| **Cloudflare Pages** | Безлимитный bandwidth, instant HTTPS   | Чуть сложнее первичная настройка  |
| **Свой домен** | GitHub Pages + CNAME в настройках репо        | Нужно купить домен                |

---

## Что внутри (структура `index.html`)

| Блок                              | Что делает                                                     |
|-----------------------------------|----------------------------------------------------------------|
| **Masthead**                       | Бренд-метка + номер выпуска (как журнал)                       |
| **Hero**                           | Полноэкранный Black Eye background, имя, роль, 4 KPI           |
| **§ I. Pipeline**                  | 3-слойная диаграмма (Pre-prod / Production / Post-prod) + 2 inter-gate |
| **§ II. Tool Spotlight · Black Eye** | Hero-кадр, 3 кадра, 6 spec cells, Adam + Gerald byline       |
| **§ III. Showcase**                 | 6 портфолио-стоп-кадров с подписями (UGC, cinema, animation, sport, art, talk) |
| **§ IV. Stack**                    | 4-колоночный грид: Pre-prod / Production / Post-prod / Scale  |
| **Footer**                         | Имя, два email, локация, год (без CTA, без формы)             |

Переключатель **RU / EN** — фиксированный в правом верхнем углу, мгновенно
переключает весь текст через `data-lang` атрибут.

---

## Известные ограничения

- **GitHub Pages — до 1 GB** на репозиторий и **до 100 MB** на один файл. Сейчас
  папка ~1.7 MB — укладывается с запасом.
- **Видео на странице нет намеренно.** Страница не грузит ни одного mp4:
  все ролики показаны стоп-кадрами. Первая загрузка — ~1.45 MB (из них ~430 KB —
  Google Fonts), картинки ниже первого экрана подгружаются лениво.
- **Проверка «страница не тянет видео»** — локально через Playwright:
  `py ../landing-scratch/verify_static.py` печатает список запросов и общий вес;
  в выводе должно быть `video_requests=0`.
- **YouTube embed** — намеренно НЕ используется, чтобы лендинг не зависел от
  внешних сервисов и YouTube-блокировок в РФ.

---

## Как обновить

1. Поправить `index.html` локально.
2. Проверить через `python -m http.server 8000`.
3. Перетащить изменённый `index.html` в репозиторий (или `git commit && git push`).
4. Через 30–60 секунд GitHub Pages задеплоит обновление.

---

## Credits

**Автор:** Антон Бычковский (Stavropol / Remote, 2026) — solo operator.
**Пайплайн:** `Mavis (M3)` — agent orchestration, развёрнут в MiniMax Code.
**Black Eye Camera** видео и логотип — © Black Eye Technologies
(Adam Myhill, Gerald Orban, Amy Zimmerman), использованы как marketing-материалы
для некоммерческого портфолио.
**Шрифты:** Playfair Display + Source Serif 4 + Inter + JetBrains Mono
(Google Fonts, Open Font License).

## Managed by Mavis (M3)

Этот лендинг обслуживается Mavis (агент M3, встроен в MiniMax Code). Push-доступ к репо через PAT в ~/.github_token. Для внесения изменений: правишь локальный index.html в C:\Users\DELL\.minimax\workspace\portfolio-prep\landing\, далее git add && git commit && git push от лица Mavis. Перед любым публичным изменением — спросить владельца (Антон Бычковский).

