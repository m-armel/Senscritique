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

## Project Structure
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

git clone https://github.com/m-armel/Senscritique.git
cd senscritique

### 2. Install dependencies

pip install -r requirements.txt

Minimal requirements:
fastapi
uvicorn
pandas
numpy
scikit-learn
sentence-transformers

### 3. Run the API

uvicorn main:app --reload

### Possible Improvements

Replace CSVs with a database (PostgreSQL, MongoDB), 
Add multilingual support for critiques

### Note

I used AI to help me with the "compute similarities" and "top-k most similar" part of the code, as i kept getting errors no matter how i twiked it.

### Author

Armel Moumbe

GitHub: @m-armel
