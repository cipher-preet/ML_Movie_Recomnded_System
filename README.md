# ML_Movie_Recomnded_System


import streamlit as st
import pickle
import pandas as pd


def recommend(movie):
    index = movies[movies['title'] == movie].index[0]
    distances = sorted(list(enumerate(similarity[index])), reverse=True, key=lambda x: x[1])

    recommended_movie_names = []

    for i in distances[1:6]:
        recommended_movie_names.append(movies.iloc[i[0]].title)
    return recommended_movie_names

# -------------------- This is pickle model file -------------------------
movies = pickle.load(open('movies.pkl','rb'))

# ---------------   This is pickle similarity file ----------------------
similarity = pickle.load(open('similarity.pkl','rb'))



#------------------------------------------------------------------------


st.title("Movie Recommended System")

movie_list  =  movies['title'].values

selected_movie  = st.selectbox(
    "How would you like to be contacted?",
    movie_list,
)

if st.button("Recommend", type="primary"):
    recommendations = recommend(selected_movie)
    for i in recommendations:
        st.write(i)
