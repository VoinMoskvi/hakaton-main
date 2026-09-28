# GreenPlan AI — автопроектирование озеленения (DXF/DWG -> DXF)

Пайплайн: вход DXF/DWG -> ограничения и допустимые зоны (СП 42.13330.2016, 743-ПП, 623-ПП/МГСН)
-> план посадок на отдельных слоях GREEN_AI_* -> интерпретации (НПА+пункт) -> смета/бюджет.

## Запуск
    pip install -r requirements.txt
    python -m app.cli doctor                 # проверка окружения и конвертера DWG
    python -m app.cli run in.dxf --out out   # прогон
    python -m app.cli serve                  # веб: http://127.0.0.1:8000 (/docs — Swagger)
    # Docker: docker compose up --build

## DWG (встроено)
Конвертер LibreDWG (dwg2dxf) кладётся в tools/:
    tools/fetch_converter.sh   (Linux)   tools/fetch_converter.bat (Windows)

## Повторный расчёт / параметры
    --seed, --territory, --budget-mode, --budget-value, --budget-policy
Результат каждого прогона — отдельно (out/), интерпретации — interpretation.json.
## Для МосТех.ОС / Ubuntu

```bash
# Установка зависимостей
sudo apt update && sudo apt install -y python3 python3-pip docker.io docker-compose-v2
# для dnf-based систем (ROSA, MosTech.OS):
# sudo dnf install -y python3 python3-pip docker docker-compose

# Локальный запуск
python3 -m pip install -r requirements.txt
python3 -m app.cli doctor
python3 -m app.cli run examples/sample_input.dxf --out out

# Docker
docker compose up --build
```

## Прогон на sample_input.dxf

```bash
python3 -m app.cli run examples/sample_input.dxf --out out --territory T1 --seed 42
# Результаты: out/result.dxf, out/interpretation.json, out/estimate.json, out/summary.json
# Эталонные выходы: examples/sample_output.dxf, examples/sample_interpretation.json
```
