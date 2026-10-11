# 🎬 Movie Recommender System – Machine Learning

**Interactive movie recommendation application** built using Python, Machine Learning, Natural Language Processing (NLP) techniques, and Streamlit. It recommends movies similar to a user's selected movie using **content-based filtering and cosine similarity**.

The project uses the **TMDB 5000 Movies and Credits datasets** and demonstrates the complete recommendation workflow, including data preprocessing, feature engineering, text vectorization, stemming, similarity calculation, and interactive movie recommendations with posters.

---

## 🎯 About the Project

The Movie Recommender System helps users discover movies based on their interests by finding titles with similar content and metadata.

The recommendation model considers:

- 🎭 Movie genres
- 🔑 Keywords
- 📝 Movie overview
- 🎬 Cast members
- 🎥 Directors

The application allows users to select a movie from a dropdown menu and receive **five similar movie recommendations**, along with their posters when available.

### Key Features

- Content-based movie recommendations
- Movie metadata preprocessing
- Text cleaning and stemming
- Feature extraction using CountVectorizer
- Cosine similarity-based recommendations
- Interactive Streamlit web interface
- Movie poster fetching through the TMDB API
- Five recommendations for each selected movie
- Graceful handling of unavailable movie posters

---

## ⚡ Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/JitendraSingh091/movie-recommender-system.git
cd movie-recommender-system
```

Replace the repository URL if you use a different repository name.

### 2. Install Dependencies

```bash
pip install numpy pandas scikit-learn nltk streamlit requests jupyter
```

### 3. Download the Dataset

Download the TMDB 5000 Movies and Credits datasets and place the CSV files in your project directory.

Required files:

```text
tmdb_5000_movies.csv
tmdb_5000_credits.csv
```

### 4. Generate the Recommendation Files

Open the Jupyter Notebook:

```bash
jupyter notebook movie-recommender-system.ipynb
```

Run the notebook cells sequentially to preprocess the dataset, create movie tags, generate feature vectors, calculate cosine similarity, and save the required model files.

The Streamlit application requires these files:

```text
movie_list.pkl
similarity.pkl
```

Ensure that the notebook's final serialization cell saves the correctly named DataFrame and similarity matrix before launching the app.

### 5. Run the Application

```bash
streamlit run main.py
```

Open the local URL displayed in your terminal, usually:

```text
http://localhost:8501
```

Select a movie and click **Show Recommendation** to view similar movies.

---

## 📊 Dataset

The project uses the **TMDB 5000 Movies and Credits datasets**.

The datasets provide movie metadata and credits that are combined using the movie title.

| Dataset column | Description |
|---|---|
| `movie_id` | Movie identifier used for poster retrieval |
| `title` | Movie title |
| `overview` | Description of the movie |
| `genres` | Movie genres |
| `keywords` | Important movie-related keywords |
| `cast` | Cast information |
| `crew` | Crew information used to extract directors |

The notebook selects the relevant columns and removes records containing missing values before feature engineering.

---

## 🧹 Data Preprocessing

The raw movie metadata is transformed into a consolidated text representation called **tags**.

### Processing Pipeline

```text
TMDB Movies Dataset
        ↓
Merge Movies and Credits
        ↓
Select Relevant Columns
        ↓
Handle Missing Values
        ↓
Extract Genres and Keywords
        ↓
Extract Top 3 Cast Members
        ↓
Extract Director
        ↓
Combine Movie Metadata
        ↓
Convert Text to Lowercase
        ↓
Apply Stemming
        ↓
Generate Movie Tags
```

### 1. Dataset Merging

The movies and credits datasets are merged using the `title` column.

### 2. Missing Values and Duplicates

The notebook checks for missing values and duplicate records. Rows with missing values are removed.

### 3. Extract Relevant Metadata

Structured genre and keyword information is converted into lists. The notebook extracts up to three cast members and identifies the director from the crew data.

### 4. Combine Movie Information

The overview, genres, keywords, cast, and director are combined into a single text field named `tags`.

### 5. Convert to Lowercase

All tags are converted to lowercase so that words with different capitalization are processed consistently.

### 6. Stemming

The project uses **PorterStemmer** from NLTK to reduce related words to their stems.

---

## 🔢 Feature Extraction

The project converts movie tags into numerical vectors using:

```python
from sklearn.feature_extraction.text import CountVectorizer

cv = CountVectorizer(
    max_features=5000,
    stop_words="english"
)

vectors = cv.fit_transform(new_df["tags"]).toarray()
```

**How it works:**

- `max_features=5000` limits the vocabulary to at most 5,000 features.
- `stop_words="english"` removes common English stop words.
- Each movie is represented by a numerical feature vector derived from its tags.

These vectors allow the recommendation algorithm to compare movie content mathematically.

---

## 🤖 Recommendation Algorithm

The project uses **Content-Based Filtering** with cosine similarity.

### 1. Content-Based Filtering

Movies are recommended based on the similarity of their metadata rather than user ratings or collaborative user behavior.

### 2. Cosine Similarity

Cosine similarity measures the similarity between two movie feature vectors.

\[
\text{Similarity}(A,B)=
\frac{A\cdot B}{\|A\|\|B\|}
\]

A higher similarity score generally indicates that the movies have more similar feature representations.

### 3. Recommendation Process

```text
User Selects a Movie
        ↓
Find Selected Movie Index
        ↓
Retrieve Similarity Scores
        ↓
Sort Movies by Similarity
        ↓
Exclude the Selected Movie
        ↓
Select Top 5 Similar Movies
        ↓
Fetch Movie Posters
        ↓
Display Recommendations
```

The recommendation function ranks the movies by similarity and returns the five highest-ranked alternatives, excluding the selected movie itself.

---

## 🖥️ Streamlit Web Application

The project includes a Streamlit interface defined in `main.py`.

### Application Features

- Movie selection through a dropdown
- Recommendation button
- Five-column recommendation display
- Movie titles
- Movie poster images
- Fallback message when a poster is unavailable

### Poster Retrieval

The application uses the TMDB API to retrieve poster paths for recommended movies.

Poster images are loaded from TMDB's image service when available. If a poster cannot be retrieved, the application displays a fallback message.

**Note:** A valid TMDB API key and an internet connection are required for live poster retrieval. Configure the API key through an environment variable rather than publishing it in source code.

---

## 🧠 Machine Learning Workflow

```text
TMDB Dataset
      ↓
Data Preprocessing
      ↓
Metadata Extraction
      ↓
Text Tag Creation
      ↓
Porter Stemming
      ↓
CountVectorizer
      ↓
Numerical Feature Vectors
      ↓
Cosine Similarity Matrix
      ↓
Rank Similar Movies
      ↓
Top 5 Recommendations
      ↓
Streamlit Application
      ↓
Movie Posters and Titles
```

---

## 🛠️ Tech Stack

| Category | Technology |
|---|---|
| Programming Language | Python |
| Data Processing | Pandas |
| Numerical Computing | NumPy |
| Machine Learning | Scikit-learn |
| Natural Language Processing | NLTK |
| Feature Extraction | CountVectorizer |
| Similarity Calculation | Cosine Similarity |
| Web Framework | Streamlit |
| HTTP Requests | Requests |
| Data Serialization | Pickle |
| Development Environment | Jupyter Notebook |
| Dataset | TMDB 5000 Movies and Credits |
| Movie Poster API | TMDB API |

---

## 📁 Repository Structure

Recommended repository structure:

```text
movie-recommender-system/
│
├── movie-recommender-system.ipynb
├── main.py
├── movie_list.pkl
├── similarity.pkl
├── requirements.txt
├── README.md
```

The two CSV dataset files are required to reproduce the notebook workflow but are not included in the structure above. Download them separately and place them in the project directory.

The `.pkl` files must be generated by the notebook or otherwise provided before running `main.py`.

---

## 📌 Key Results

The project demonstrates how movie metadata can be transformed into feature vectors and used to identify similar movies.

- Combines five categories of movie information into a unified tag representation.
- Uses a vocabulary of up to 5,000 features.
- Computes cosine similarity between movie vectors.
- Returns five similar movies for a selected title.
- Displays movie posters through the TMDB API when available.

This is a content-based recommendation system, not a rating-prediction model. Its recommendation quality depends on the available metadata and the quality of the feature representation.

---

## 🚀 Future Improvements

Possible future enhancements include:

- Add genre and language filters.
- Display movie ratings, release years, and descriptions.
- Add search functionality beyond the dropdown.
- Improve the interface with custom CSS and responsive layouts.
- Add movie recommendation explanations.
- Optimize similarity lookup for larger datasets.
- Add unit tests and error handling.
- Cache poster requests to reduce repeated API calls.
- Add recommendation evaluation metrics.
- Compare CountVectorizer with TF-IDF.
- Add collaborative filtering using user ratings.
- Deploy the application using Streamlit Community Cloud or another hosting platform.
- Add personalized recommendations based on user preferences.

---

## 📸 Project Preview

Add screenshots of your running Streamlit application to the repository.

Example:

```text
📸 Movie Selection Interface
📸 Recommended Movie Titles
📸 Movie Poster Display
📸 Complete Streamlit Application
```

Once you upload a screenshot to the `screenshots/` folder, display it in the README using:

```markdown
![Movie Recommender System](screenshots/app-preview.png)
```

---

## 👨‍💻 Author

**Jitendra Singh**

B.Tech – Computer Science & Engineering

Data Science | Machine Learning | Artificial Intelligence

### 🔗 GitHub

[github.com/JitendraSingh091](https://github.com/JitendraSingh091)

---

## 📄 License

This project can be distributed under the MIT License if you choose to include that license. Add a `LICENSE` file containing the appropriate license text before describing the repository as MIT-licensed.

---

## 🏷️ GitHub Topics

Suggested repository topics:

```text
movie-recommender-system
movie-recommendation
content-based-filtering
machine-learning
python
streamlit
scikit-learn
pandas
numpy
nltk
cosine-similarity
countvectorizer
tmdb
data-science
jupyter-notebook
```

---

## 📬 Feedback

Suggestions and contributions are welcome. Feel free to open an Issue or submit a Pull Request to improve the project.

⭐ If you find this project useful, consider giving the repository a star!
