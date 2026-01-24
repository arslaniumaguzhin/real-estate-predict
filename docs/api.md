Base URL (local):
- `http://127.0.0.1:8000`

Data format:
- JSON
- Content-Type: application/json

---


POST /predict
Назначение: получить оценку стоимости квартиры по параметрам

Request JSON
Поля:

area (number) — площадь кв.м, > 0

rooms (integer) — число комнат, >= 0 (0 = студия)

metro_station (string) — ближайшая станция метро (название)

Пример:

{
  "area": 80,
  "rooms": 2,
  "metro_station": "Киевская"
}

Response 200 JSON
Поля:

price_total (number) — итоговая цена  рублях

currency (string) — "RUB"

price_per_sqm (number, optional) — цена в рублях за 1 м²

model_version (string) - версия модели нейросети

Пример:

{
  "price_total": 7500000,
  "currency": "RUB",
  "price_per_sqm": 93750,
  "model_version": "v0.1"
}

Errors
Единый формат ошибок:

error (string)

message (string)

details (object, optional)

422 validation_error
{
  "error": "validation_error",
  "message": "Invalid input data",
  "details": {
    "area": "must be > 0",
    "rooms": "must be >= 0",
    "metro_station": "must be non-empty"
  }
}

500 internal_error
{
  "error": "internal_error",
  "message": "Unexpected error"
}
