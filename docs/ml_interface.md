Backend вызывает ML как Python-функцию. ML не делает input()/print(), только чистые функции.

---

Backend передаёт структуру:

- `area` (float) — > 0
- `rooms` (int) — >= 0 (0 = студия)
- `metro_station` (str) — non-empty (после редактирования с помощью `strip()`)


Python example:

features = {
  "area": 80.0,
  "rooms": 2,
  "metro_station": "Киевская"
}


Output (prediction)

ML возвращает структуру:

price_total (float)  — цена в рублях

price_per_sqm (float | None, optional) — цена в рублях за 1 м²

model_version (str) - версия модели нейросети

Python example:

result = {
  "price_total": 7500000.0,
  "price_per_sqm": 93750.0,
  "model_version": "v0.1"
}

Function contract
from typing import TypedDict, Optional

class Features(TypedDict):
    area: float
    rooms: int
    metro_station: str

class Prediction(TypedDict):
    price_total: float
    price_per_sqm: Optional[float]
    model_version: str

def predict(features: Features) -> Prediction:
    ...

Errors

При некорректном вводе ML бросает ValueError("...").

Backend ловит это и возвращает 422 validation_error по docs/api.md.
