# AIWAY — CLAUDE.md

## 1. Обзор проекта

**AIWAY** — лендинг ИИ-агентства автоматизаций для бизнеса (РФ).
Предложение: ИИ-агенты на подписке (8 000–90 000 ₽/мес) для любых ниш — маркетплейсы, CRM, HR, юристы, отели, рестораны и др.

**Технический стек:**
- `index.html` — главная страница, весь HTML + CSS (`<style>`) + JS (`<script>`) в одном файле (~1345 строк)
- `privacy.html` — Политика конфиденциальности (отдельная страница, noindex)
- `offer.html` — Договор-оферта (отдельная страница, noindex)
- Lucide Icons через CDN (`unpkg.com/lucide@latest`)
- Google Fonts: Space Mono, Barlow, Barlow Condensed
- Никаких фреймворков, сборщиков, npm-пакетов
- Язык контента: **русский**, валюта: **рубли (₽)**

**Как запустить:** открыть `index.html` в браузере напрямую.

**Структура файлов:**
```
AIWAY/
├── index.html      ← главная страница (~1345 строк)
├── privacy.html    ← Политика конфиденциальности
├── offer.html      ← Договор-оферта
└── CLAUDE.md       ← этот файл
```

---

## 2. Архитектура и ключевые файлы

### `index.html` — структура

| Диапазон строк | Что там |
|---|---|
| 1–11 | `<head>`: мета-теги, Google Fonts, Lucide CDN |
| 12–600 | `<style>`: CSS (переменные → ресет → компоненты → секции → медиазапросы) |
| 601–1183 | `<body>`: HTML-разметка всех секций + footer |
| 1185–1345 | `<script>`: JS (Lucide init, scroll reveal, nav state, tabs, FAQ, consent, form submit, input mask) |

### Секции страницы

| ID | Секция | Номер тега |
|---|---|---|
| `#hero` | Хиро — заголовок ПОКА КОНКУРЕНТЫ ДУМАЮТ + 3 trust-утверждения справа | — |
| `#niches` | Для кого — 2 больших карточки (Клиентский сервис / Внутренние процессы) | 03 |
| `#services` | Услуги — 6 вкладок (Флагман, Маркетплейсы, Продажи и CRM, Контент, Разработка, Интеграция), 18 услуг | 04 |
| `#how` | Как работаем — 4 шага | 05 |
| `#cases` | Кейсы — 3 карточки (маркетплейс, недвижимость, право) | 06 |
| `#faq` | Вопросы — аккордеон, 5 вопросов | 07 |
| `#cta` | Получить пилот — форма заявки + чекбокс согласия | 08 |
| `footer` | Футер — логотип, ссылки, реквизиты ИП, ссылки на privacy/offer | — |

### `privacy.html` / `offer.html`
- Самостоятельные страницы со своим `<style>` (копия CSS-переменных + стили для юридического текста)
- Навбар идентичен главной, ссылки ведут на `index.html#секция`
- `<meta name="robots" content="noindex, nofollow">`
- Реквизиты: ИП Тимофеев Даниил Сергеевич, ИНН 781140688050, ОГРНИП 325784700190518

---

## 3. Дизайн-система

### CSS-переменные (`:root`)

```css
--bg:        #080810;    --bg2:       #0D0D1A;    --bg3:       #12121F;
--line:      rgba(255,255,255,0.07);   --line2: rgba(255,255,255,0.14);
--muted:     #4A4A6A;    --sub:       #7A7A9A;    --body-c:    #B0B0C8;
--head:      #E8E8F0;    --white:     #F0F0F8;
--cyan:      #00E5FF;    --cyan-dim:  rgba(0,229,255,0.06);  --cyan-mid: rgba(0,229,255,0.15);
--green:     #00FF88;    --red:       #FF3B3B;
```

### Шрифты

| Семейство | Назначение |
|---|---|
| `'Barlow Condensed'` (900/700/600/300) | Крупные заголовки, логотип |
| `'Barlow'` (300–700) | Основной текст, описания |
| `'Space Mono'` (400/700) | Метки, цены, кнопки, навигация, теги секций |

### Чередование фонов

```
Hero     → --bg
Niches   → --bg
Services → --bg2
How      → --bg
Cases    → --bg2
FAQ      → --bg2
CTA      → --bg
Footer   → --bg + border-top
```

---

## 4. Соглашения по коду

### CSS-классы — префиксный паттерн `{компонент}-{элемент}`

| Компонент | Примеры классов |
|---|---|
| Навигация | `.nav-logo`, `.nav-brand`, `.nav-tagline`, `.nav-links`, `.nav-cta` |
| Ниши | `.niches-grid`, `.niche-card`, `.niche-title`, `.niche-desc`, `.niche-label`, `.niche-list`, `.niche-clients` |
| Услуги | `.services-tabs`, `.stab`, `.services-panel`, `.srv-header`, `.srv-row`, `.srv-num`, `.srv-name`, `.srv-desc`, `.srv-price`, `.srv-featured` |
| Шаги | `.steps`, `.step`, `.step-bg-num`, `.step-tag`, `.step-title`, `.step-desc`, `.step-time` |
| Кейсы | `.cases-grid`, `.case-card`, `.case-niche`, `.case-pain`, `.case-label` |
| FAQ | `.faq-list`, `.faq-item`, `.faq-q`, `.faq-q-text`, `.faq-icon`, `.faq-a` |
| CTA/Форма | `.cta-inner`, `.cta-title`, `.cta-box`, `.cta-form`, `.form-input`, `.form-submit`, `.consent-block` |
| Футер | `.footer-inner`, `.footer-logo`, `.footer-links`, `.footer-right`, `.footer-requisites`, `.footer-legal`, `.footer-meta` |

### Утилиты

```css
.tag           /* метка секции: "03 // Для кого" */
.sec-title     /* заголовок секции */
.sec-sub       /* подзаголовок секции */
.sec-sub-hero  /* крупный белый подзаголовок (в Niches) */
.btn-primary   /* кнопка-CTA — cyan bg, стрелка → через ::after */
.btn-outline   /* вторичная кнопка */
.reveal        /* scroll-анимация (opacity:0 → 1 + translateY) */
.container     /* max-width:1200px, padding:0 3rem */
```

---

## 5. Ключевые компоненты

### Навигация
- `position: fixed`, `z-index: 500`, высота 58px
- Логотип: SVG + `AI<span>WAY</span>` + подстрочник `ИИ-агентство автоматизаций`
- На `<640px` `.nav-links` скрыты
- Меню: Ниши | Услуги | Процесс | Кейсы | Вопросы | [Получить пилот]

### Hero
- Двухколоночный `hero-bottom`: слева описание + CTA, справа 3 trust-утверждения с ✦
- На `<900px` складывается в 1 колонку

### Услуги — 6 вкладок
- Вкладки: Флагман (cat0, active по умолчанию), Маркетплейсы (cat1), Продажи и CRM (cat2), Контент (cat3), Разработка (cat4), Интеграция (cat5)
- Таблица: 5 колонок — `#`, `Услуга`, `Что делает агент`, `Установка`, `Подписка / мес`
- Флагман выделен: `.srv-featured` — cyan border-left + cyan-dim фон
- На `≤1100px` колонки цен скрываются; на `≤640px` остаются только `#` и `Услуга`

### FAQ — аккордеон
- `.faq-item.open` → cyan border-left, белый цвет вопроса, `+` поворачивается на 45°
- Открывается один пункт одновременно

### Форма заявки
- Webhook: `https://hook.eu1.make.com/w0rzwqetf2gfdz0uqe6t7bcg9xdguhiv` (POST, mode: no-cors, Content-Type: text/plain)
- Поля: `#fname` (имя), `#fniche` (ниша), `#fcontact` (телефон/Telegram)
- Чекбокс `#consentCheck` — кнопка disabled пока не отмечен
- Маска `#fcontact`: автоопределение phone/telegram по первому символу, форматирование `+7 (XXX) XXX-XX-XX` или `@username`

### Scroll Reveal
- `IntersectionObserver`, threshold: 0.06
- `.reveal` → `.visible` при пересечении

---

## 6. Заметки для разработки

### Критичные зависимости
- Google Fonts (CDN) — офлайн деградируют
- Lucide Icons (CDN `unpkg.com`) — нужен интернет
- CSS-переменные повсеместно — **никогда не хардкодить hex-цвета**

### Подводные камни

1. **`btn-primary::after { content: '→'; }`** — стрелка через CSS, не дублировать в HTML
2. **`.nav-cta` через `!important`** — JS пропускает её при подсветке активных ссылок
3. **Таблица услуг: 5 колонок** — на `≤1100px` скрываются колонки 4-5 (цены), на `≤640px` скрываются колонки 3-5
4. **Форма отправляет на Make.com webhook** — `mode: 'no-cors'`, ответ не читается (opaque response)
5. **Маска телефона перехватывает Backspace** через `e.preventDefault()` в keydown — не добавлять свои обработчики на `#fcontact`
6. **`body::before` (scanlines) — `z-index: 1000`** — выше навигации, так задумано
7. **Блок Packages удалён** — нет тарифных карточек, цены только в таблице услуг

### Адаптив — три брейкпоинта

| Брейкпоинт | Основные изменения |
|---|---|
| `≤1100px` | Таблица услуг: 3 колонки (без цен) |
| `≤900px` | Hero в 1 колонку; ниши в 1 колонку; шаги 2×2; CTA в столбец |
| `≤640px` | Навигация без ссылок; всё в 1 колонку; форма в 1 колонку |

### Юридические страницы
- `privacy.html` и `offer.html` — самостоятельные, CSS встроен
- Ссылки из главной: `privacy.html`, `offer.html` (относительные, не `/privacy`)
- Реквизиты ИП дублируются в footer и на юр. страницах

### Telegram
- Кнопка «Написать в Telegram»: `https://t.me/aiway_agency`
- Email: `ai@aiway.agency`
