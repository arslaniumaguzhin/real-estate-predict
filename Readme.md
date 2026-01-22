## Для Backend (Arslan)
cd backend
.venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8000

## Для Frontend
cd frontend
npm install
npm start  # localhost:3000

## Для ML
cd ml
python -m venv .venv
.venv\Scripts\activate
pip install scikit-learn pandas jupyter  # пример
jupyter notebook  # для экспериментов

Test protection