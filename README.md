# Movie-recommender-system
Developed a content-based movie recommender using cosine similarity on textual movie features, deployed as an interactive web application using Streamlit.
movie-recommender/
│
├── app.py
├── movie_list.pkl
├── similarity.pkl   (if using it)
├── requirements.txt
├── README.md
└── .gitignore
1️⃣ app.py
import streamlit as st
import pickle
import pandas as pd

# Load data
movies = pickle.load(open('movie_list.pkl', 'rb'))
similarity = pickle.load(open('similarity.pkl', 'rb'))

def recommend(movie):
    index = movies[movies['title'] == movie].index[0]
    distances = sorted(list(enumerate(similarity[index])), reverse=True, key=lambda x: x[1])
    
    recommended_movies = []
    for i in distances[1:6]:
        recommended_movies.append(movies.iloc[i[0]].title)
    return recommended_movies


st.title('🎬 Movie Recommender System')

selected_movie = st.selectbox(
    "Select a movie",
    movies['title'].values
)

if st.button('Recommend'):
    recommendations = recommend(selected_movie)
    for movie in recommendations:
        st.write(movie)
2️⃣ requirements.txt
streamlit
pandas
numpy
scikit-learn
3️⃣ README.md
# 🎬 Movie Recommender System

This is a Content-Based Movie Recommendation System built using Python and Streamlit.

## 🚀 Features
- Select any movie from dropdown
- Get top 5 similar movie recommendations
- Built using cosine similarity

## 🛠 Tech Stack
- Python
- Pandas
- Scikit-learn
- Streamlit

## 📂 Files
- app.py → Main Streamlit app
- movie_list.pkl → Processed movie dataset
- similarity.pkl → Cosine similarity matrix
- requirements.txt → Dependencies

## ▶️ Run Locally

```bash
pip install -r requirements.txt
streamlit run app.py
🌐 Live Demo

---

# 📌 4️⃣ .gitignore

Create this file:
pycache/
*.pyc
.env

---

# 📌 5️⃣ How To Upload To GitHub

### Step 1:
Go to GitHub → New Repository  
Name: `movie-recommender`

### Step 2:
Upload all files

OR using Git:

```bash
git init
git add .
git commit -m "Initial commit - Movie Recommender"
git branch -M main
git remote add origin https://github.com/yourusername/movie-recommender.git
git push -u origin main

        
