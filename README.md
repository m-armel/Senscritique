# Critique Recommendation System (SensCritique Test)

This project implements a recommendation feature for **SensCritique**:  
when a user reads a critique of a film, the system suggests **similar critiques from the same film**.

---

## Features
- FastAPI backend with a `/similar-critiques` endpoint
- Semantic embeddings using [SentenceTransformers](https://www.sbert.net/) (`all-MiniLM-L6-v2`)
- Cosine similarity for ranking critiques
- Works with provided datasets (`fightclub_critiques.csv`, `interstellar_critiques.csv`)
- Preprocessing (lowercasing, punctuation cleanup)
- Embedding cache (`embeddings.npy`) for faster startup

---

### Flow
1. User reads a critique in the frontend.  
2. Frontend calls the API:  
3. API retrieves the target critique, restricts search to the same film.  
4. Precomputed embeddings are used to calculate **cosine similarity**.  
5. Returns the **top-k most similar critiques**.  

---

## 📂 Project Structure
.
├── fightclub_critiques.csv
├── interstellar_critiques.csv
├── main.py # FastAPI application
├── embeddings.npy # Cached embeddings (auto-created)
├── docs/
└── README.md

---

## Installation

### 1. Clone the repo

git clone https://github.com/m-armel/Senscritique/tree/main
cd senscritique-reco

2. Install dependencies
pip install -r requirements.txt
Minimal requirements:
fastapi
uvicorn
pandas
numpy
scikit-learn
sentence-transformers

3. Run the API
uvicorn main:app --reload

📌 Usage Example
Request
GET http://127.0.0.1:8000/similar-critiques?critique_id=1&top_k=3
Response
[
  {
    "id": 2,
    "film_id": 101,
    "texte": "Violence gratuite, pas mon style",
    "similarité": 0.81
  },
  {
    "id": 4,
    "film_id": 101,
    "texte": "Les combats sont trop longs",
    "similarité": 0.78
  }
]

Possible Improvements

Replace CSVs with a database (PostgreSQL, MongoDB)
Add multilingual support for critiques

Author
Armel Moumbe
GitHub: @m-armel
