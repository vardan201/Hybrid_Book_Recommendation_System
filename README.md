** THE PROJECT WAS BUILT ON GOOGLE COLAB

# 📚 Hybrid Book Recommendation System

This project is a **Hybrid Book Recommender System** built using Python . It leverages a combination of:
- ✅ **Content-Based Filtering** using TF-IDF vectorization over book metadata (like descriptions or summaries), and
- ✅ **Collaborative Filtering** using matrix factorization via the **SVD algorithm** from the `scikit-surprise` library.

This hybrid approach provides **highly personalized and relevant book suggestions** based on both what the book is about and how similar users have rated it.

---
## 🎯 Project Goal

To develop a scalable and accurate recommendation engine that suggests books based on user preferences, book content, and global rating patterns. The system is capable of handling both **cold-start** cases (new books or users) and well-rated entries.

---
## 💡 Key Features

- 🔍 **Search Any Book** – Get top N recommendations by typing in the title.
- 📖 **Hybrid Recommendations** – Merges both content similarity and collaborative predicted ratings.
- 📊 **Optimized SVD Model** – GridSearchCV was used to tune the SVD parameters for better accuracy.
- ⚡ **TF-IDF Based Content Matching** – Uses cosine similarity on vectorized book descriptions.
- 🎯 **Fallback Logic** – If a book has no ratings, content similarity alone is used.

## 📁 Directory Structure

├── Collaborative_Filtering # collaborative filtering model
├── Content_similarity # logic for content similarity
├── Hybrid_Recommendations # hybrid recommendation system logic
├── svd_model.pkl # Trained SVD model (collaborative filtering)
├── tfidf_matrix.pkl # TF-IDF vectorized content data
├── requirements.txt # Required packages
└── README.md # Project documentation

📊 Dataset Details
🔹 books_cleaned.csv
Contains cleaned metadata of books including book_id, title, author, content or description (used for TF-IDF), etc.

Titles are preprocessed to lowercase to standardize input matching.

🔹 ratings.csv
Contains user ratings in the form: user_id, book_id, rating.

Used to train the SVD model for collaborative filtering.


---

## 🔧 Installation and Setup

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/yourusername/hybrid-book-recommender.git
cd hybrid-book-recommender

2️⃣ Install Requirements

pip install -r requirements.txt
🧠 How the Recommendation Engine Works
💬 Input: A book title
When a user inputs a book title, the system performs the following:

1. Content-Based Filtering (CBF)
The content (summary/description) of each book is vectorized using TF-IDF.

Cosine similarity is computed between the selected book and all other books.

Top similar books are shortlisted.

2. Collaborative Filtering (CF)
If the selected book and candidate books have enough user ratings, the SVD model predicts how much a similar user would rate the candidate book.

3. Hybrid Score Calculation
Each candidate book gets a hybrid score calculated as:

python
Copy
Edit
hybrid_score = (cosine_similarity * 5 + predicted_rating) / 2
cosine_similarity is scaled to match the rating scale (0–5).

If collaborative filtering data is missing, the fallback is just: hybrid_score = cosine_similarity * 5.

4. Top N Recommendations
The top N books with the highest hybrid scores are displayed.


📘 Hybrid Recommendations for 'Bagombo Snuff Box':
1. The Welcome To The Monkey House (Hybrid Score: 4.75)
2. Slaughterhouse Five (Hybrid Score: 4.68)
3. Cat's Cradle (Hybrid Score: 4.57)
...



