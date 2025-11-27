# Проектный практикум УРФУ

## Предварительная настройка

После клонирования проекта необходимо сделать следующее

Создать или обновить окружение:
```bash
conda env create -f environment.yml     # если окружения ещё нет
# или
conda env update -f environment.yml     # если окружение уже создано
```
Активировать окружение:
```bash
conda activate obesity-risk
```
Установить проект как Python-пакет (обязательно,  иначе нельзя будет импортировать внутренние библиотеки проекта utils.py):
```bash
pip install -e . # с точкой
```

## Установка зависимостей в Conda

Не обязательно, но упрощает работу - с помощью Conda можно установить разом все необходимые для работы с проектом библитеки. Подходит для macOS, Linux и Windows. Библиотеки с указанием версии перечислены в файле окружения: `environment.yml` - лежит в корне проекта.

### Mac (Linux)

Если не установлена Conda, устанавливаем:
```bash
brew install --cask miniconda
```
Активируем и перезагружаем терминал:
```bash
conda init zsh
exec zsh
```

Создаем окружение из `environment.yml` (нужно делать из папки с этим файлом):
```bash
conda env create -f environment.yml
conda activate obesity-risk
```

- Обновить окружение после правок `environment.yml`:

```bash
conda env update -f environment.yml --prune
```

### Windows

Выполните команды в Anaconda Prompt или в PowerShell с активированной инициализацией conda.

`conda activate obesity-risk` работает в Anaconda Prompt и в PowerShell после `conda init powershell`.


## Подготовка данных

Утилиты загрузки и очистки данных находятся в `src/utils.py`.

Основные функции:

- `load_raw_df()` — загружает сырой CSV из `data/raw`.
- `load_clean_df()` — загружает и очищает (удаляет дубли и прочее).

Пример запуска из корня проекта (можно использовать и внутри ноутбуков):

```python
from src.utils import load_raw_df, load_clean_df

df = load_raw_df()
df_clean = load_clean_df()
```

Если в эти функции подставить 'short_names' или 'long_names', то будет сформирован датафрей с соответствующим наименованиям столбцов на русском:

```python
from src.utils import load_raw_df, load_clean_df

df = load_raw_df('short_names')
df_clean = load_clean_df('short_names')
```

Меняйте логику очистки в `load_clean_df` в `src/utils.py`, если нужно и централизованно.