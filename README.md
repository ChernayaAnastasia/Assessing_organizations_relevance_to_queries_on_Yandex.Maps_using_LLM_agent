# Assessing Organizations Relevance to Queries on Yandex.Maps using LLM Agent
(Оценка релевантности организаций запросам на Яндекс.Картах с помощью LLM-агента)

**📍 Итоговый проект курса NLP школы Deep Learning School**  
**🎯 Цель:** Построение LLM-агента, который оценивает релевантность организаций на Яндекс.Картах широким пользовательским запросам. Его сравнение с сильным бейзлайном.

---

## 🔍 Описание проекта

Проект направлен на исследование и реализацию подходов с использованием больших языковых моделей (LLM) для задачи **оценки релевантности** организаций запросам пользователей в геосервисе.  
LLM-агент анализирует входные данные (запрос и информацию об организации), при необходимости запрашивает дополнительный контекст через поиск, и выдает бинарное решение: **релевантна ли организация запросу**.

Модель протестирована на различных промптах и версиях агентов и сравнивается с бейзлайном.

---

## 📁 Структура репозитория

```bash
llm_relevance_agent/
├── baseline/                  # Бейзлайн-модель на GPT без внешнего поиска
│   ├── llm_interface.py       # Обёртка над OpenAI API
│   ├── prompt_templates.py    # Промты для бейзлайна
│   ├── core.py                # Класс RelevanceBaseline
│   └── run_baseline.py        # Запуск бейзлайна 
│
├── agent/                     # Реализация LLM-агента
│   ├── prompts/               # Разные версии промтов
│   ├── agent_graph.py         # Граф агента на langgraph
│   ├── agent_nodes*.py        # Узлы графа (версии)
│   ├── eval_agent.py          # Модуль RelevanceAgentEvaluator для оценки агента
│   ├── promt_loader.py        # Загрузка промтов по версии
│   └── search_tools.py        # Интеграция поиска (Tavily)
│
├── data/                      # Датасеты 
│   ├── data_final_for_dls.jsonl   
│   └── data_final_for_dls_new.jsonl 
│
├── experiments/               # Предсказания, логи и анализ
│   ├── agent/                 # Предсказания разных версий агента
│   │   ├── *.csv              # Предсказания
│   │   ├── agent_error_analysis.ipynb  # Анализ ошибок агента и выводы проекта 
│   │   ├── run_agent_ipynb.ipynb   # Для запуска бейзлайна в Jupiter Notebook 
│   │   ├── agent_logs/
│   │   ├── analysis_errors/
│   │   ├── search_cache_v1/
│   │   └── search_cache_v3/
│   ├── baseline_test_predictions.csv
│   ├── baseline_val_predictions.csv
│   ├── run_baseline_pipeline.ipynb  # Для запуска агента в Jupiter Notebook 
│   ├── baseline_val_errors_analysis.ipynb
│   └── baseline_val_predictions_old.csv
│
├── utils/                     # Утилиты
│   ├── data_loader.py
│   ├── config.py
│   ├── inspector.py
│   ├── unify_columns.py
│   └── __init__.py
│
├── requirements.txt           # Зависимости pip
├── environment.yml            # Зависимости conda
├── .env                       # Ключи API и конфигурации
└── main_runner.py             # Основной вход для запуска агента
```

### 🚀 Быстрый старт

Загрузить [данные](https://drive.google.com/file/d/1WADIWzvNcQTA6X4FGYKV6f0m1z0URYhj/view?usp=sharing)

#### Установить зависимости

conda env create -f environment.yml

conda activate llm_relevance

#### Запустить бейзлайн
python baseline/run_baseline.py --batch_size 5 --output_prefix baseline

или через ноутбук:
experiments/run_baseline_pipeline.ipynb

#### Запустить агента
python llm_relevance_agent/main_runner.py --batch_size 5

или через ноутбук:
experiments/agent/run_agent_ipynb.ipynb

