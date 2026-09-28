# Промышленное наследие РФ

<p align="left">
  <img src="https://img.shields.io/badge/Python-3.11%2B-3776AB?style=flat&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/FastAPI-0.136-009688?style=flat&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/Streamlit-1.57-FF4B4B?style=flat&logo=streamlit&logoColor=white" alt="Streamlit" />
  <img src="https://img.shields.io/badge/Three.js-r128-000000?style=flat&logo=threedotjs&logoColor=white" alt="Three.js" />
  <img src="https://img.shields.io/badge/OpenAI_API-GPT--4o--mini-412991?style=flat&logo=openai&logoColor=white" alt="OpenAI" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat" alt="MIT License" />
</p>

Система автоматизированного подбора инвестиционных площадок и предиктивного проектирования заводов сэндвич-панелей в субъектах РФ. На основе заданных параметров инвестора выполняет скоринг регионов, рассчитывает CAPEX/OPEX, формирует интерактивную 3D-модель площадки, генерирует фасадные AI-рендеры и собирает инвестиционный PDF-меморандум.

---

## 🛠 Технологический стек

| Категория | Технологии | Назначение |
| :--- | :--- | :--- |
| **Backend Core** | `Python 3.11+`, `FastAPI`, `Uvicorn`, `Pydantic v2` | Асинхронный REST API, валидация схем данных, бизнес-логика |
| **Data Engine & Math** | `Pandas`, `NumPy` | Обработка региональных датасетов, скоринговая матрица, расчет баланса площадей и смет |
| **Frontend & GIS** | `Streamlit`, `Folium`, `Streamlit-Folium`, `Plotly` | Интерактивный дашборд, геопространственная карта поставок, аналитические графики |
| **3D & Visualization** | `Three.js (WebGL)`, `HTML5 Canvas`, `Jinja2` | Процедурная генерация интерактивного 3D-генплана предприятия в браузере |
| **Generative AI** | `OpenAI API (GPT-4o-mini / ProxyAPI)`, `DALL-E` | Концептуализация региональной стилистики, экономическая аналитика, рендеринг фасадов |
| **Document Processing** | `FPDF2`, `FreeSans / Times TTF` | Программная сборка многостраничных инвестиционных PDF-презентаций |
| **DevOps & Deploy** | `Docker`, `Docker Compose`, `Git` | Контейнеризация сервисов, изоляция среды |

---

## ⚡ Функциональные возможности

- **Многофакторный скоринг площадок**: фильтрация и ранжирование по 25+ метрикам (логистика, тарифы, налоги, кадры, сырье).
- **Инженерно-экономический расчет**: расчет площадей корпусов, инфраструктуры и CAPEX/OPEX с климатическими поправками.
- **Интерактивный 3D-генплан**: генерация трехмерной модели площадки (цех, склад, АБК, парковка, благоустройство) на Three.js.
- **AI-генерация архитектурных решений**: синтез концепта и рендеринг 4 фасадов (Юг, Север, Запад, Восток) с учетом стилей региона.
- **Экспорт инвестиционного буклета**: автоматическая сборка PDF-презентации со сводкой, картой, расчетами и визуализациями.
- **ГИС-аналитика**: интерактивная карта радиусов логистики, плеч доставки металлопроката и утеплителя.

---

## 🏗 Архитектура решения

```
┌─────────────────────────────────────────────────────────────────┐
│                    Streamlit Frontend (UI / GIS)                │
│  - Интерактивная карта (Folium)   - 3D Viewer (Three.js / HTML) │
│  - Форма параметров инвестора     - Графики и сравнение (Plotly)│
└────────────────────────────────┬────────────────────────────────┘
                                 │ HTTP JSON
┌────────────────────────────────▼────────────────────────────────┐
│                    FastAPI Backend (Core Engine)                │
│  - calculator.py (CAPEX / СНиП)   - pdf_service.py (FPDF2)      │
│  - llm_service.py (Аналитика)     - render_service.py (AI Фасад)│
└────────────────┬───────────────────────────────┬────────────────┘
                 │                               │
        ┌────────▼────────┐             ┌────────▼────────┐
        │  OpenAI / Proxy │             │   data.csv      │
        │  (GPT / Image)  │             │   (База данных) │
        └─────────────────┘             └─────────────────┘
```

---

## 📁 Структура проекта

```text
industrial-heritage/
├── backend/
│   ├── app.py                # Маршрутизатор FastAPI и эндпоинты
│   ├── calculator.py         # Алгоритмы расчета площадей, стоимости и скоринга
│   ├── data_loader.py        # Парсинг и нормализация региональных данных
│   ├── llm_service.py        # Интеграция с LLM для концептов и аналитики
│   ├── models.py             # Pydantic-модели запросов и форм
│   ├── pdf_service.py        # Компоновка и верстка PDF-отчетов
│   ├── render_service.py     # Генерация и кэширование AI-фасадов
│   ├── three_d_generator.py  # Процедурный генератор Three.js сцены
│   └── data.csv              # Базовый датасет параметров субъектов РФ
├── frontend/
│   └── streamlit_app.py      # Клиентский веб-интерфейс на Streamlit
├── static/
│   └── three_scene.html      # Базовый WebGL/HTML5 шаблон 3D-сцены
├── requirements.txt          # Зависимости Python
├── .gitignore                # Исключения версионирования
└── README.md
```

---

## ⚙️ Конфигурация (.env)

Создайте файл `.env` в корне проекта:

```env
OPENAI_API_KEY=sk-your-openai-key
OPENAI_BASE_URL=https://openai.api.proxyapi.ru/v1
BACKEND_HOST=127.0.0.1
BACKEND_PORT=8000
```

---

## 🚀 Быстрый запуск

### Вариант 1: Локально (Native)

#### 1. Подготовка окружения
```bash
# Создание виртуального окружения
python -m venv .venv

# Активация окружения (Windows PowerShell):
.venv\Scripts\Activate.ps1
# Активация окружения (Linux/macOS):
source .venv/bin/activate

# Установка зависимостей
pip install --upgrade pip
pip install -r requirements.txt
```

#### 2. Запуск Backend (FastAPI)
```bash
cd backend
python -m uvicorn app:app --host 127.0.0.1 --port 8000 --reload
```
API: [http://127.0.0.1:8000](http://127.0.0.1:8000) | Docs: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

#### 3. Запуск Frontend (Streamlit)
*В новом окне терминала (с активным `.venv`):*
```bash
cd frontend
streamlit run streamlit_app.py
```
Интерфейс: [http://localhost:8501](http://localhost:8501)

---

### Вариант 2: Запуск в Docker

```bash
docker compose up --build
```

---

## 📡 Ключевые эндпоинты API

| Метод | URL | Назначение |
| :--- | :--- | :--- |
| `POST` | `/api/analyze` | Скоринг базы регионов, отбор Топ-3 и генерация концепта |
| `POST` | `/api/all_alternatives` | Расчет параметров по всем площадкам датасета |
| `POST` | `/api/renders` | Генерация 4 ракурсов фасадов через AI-пайплайн |
| `POST` | `/api/pdf_with_renders` | Сборка PDF-презентации с обновленными рендерами |
| `GET` | `/api/download_pdf/{site_id}` | Скачивание готового PDF-файла площадки |
