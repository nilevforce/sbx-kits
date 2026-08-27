# sbx-kit-pi-deepseek

Kit для Docker Sandboxes (`sbx`), который запускает агента [Pi](https://pi.dev) с [DeepSeek](https://platform.deepseek.com) в качестве провайдера модели. Реальный API-ключ остаётся на хосте; sandbox видит только сентинел `proxy-managed` — прокси на стороне хоста подставляет настоящий ключ в исходящие запросы к `api.deepseek.com`.

## Требования

- Установленный [Docker Sandboxes (`sbx`)](https://docs.docker.com/ai/sandboxes/install/), выполнен вход (`sbx login`)
- API-ключ DeepSeek с [platform.deepseek.com](https://platform.deepseek.com/api_keys)

## Использование

### 1. Сохрани свой API-ключ DeepSeek

```bash
sbx secret set deepseek
```

Запросит значение и сохранит его в системном keychain. По умолчанию ключ глобальный — доступен любому sandbox'у, созданному из этого kit'а.

### 2. Разреши источник этого kit'а (только один раз)

```bash
sbx settings set kit.allowedSources '["docker.io/","github.com/nilevforce/"]'
```

Замени `nilevforce` на тот аккаунт, куда ты запушил репозиторий. Если у тебя уже разрешены другие источники — добавь этот к существующему списку, а не перезаписывай его.

### 3. Запусти

```bash
sbx run --kit "git+https://github.com/nilevforce/sbx-kits.git#dir=pi/deepseek" pi-deepseek
```

Первый запуск установит Pi через npm внутри sandbox — займёт чуть больше времени. Дальше сразу попадёшь в терминальный интерфейс Pi.

### Повторный запуск существующего sandbox'а

```bash
sbx run pi-deepseek
```

Или разовая команда без входа внутрь:

```bash
sbx exec pi-deepseek -- <команда>
```

### Выбор модели

Внутри Pi:
