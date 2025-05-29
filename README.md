## Features

* **Content-Based Filtering**: Recommends movies based on textual content similarity.
* **Interactive UI**: Built with Streamlit for easy user interaction.
* **Customizable Recommendations**: Users can specify the number of recommendations they want.

## How It Works

1.  **Data Preprocessing (`preprocess_data.py`)**:
    * Loads movie data from `rotten_tomatoes_movies.csv`.
    * Cleans the data (handles missing values, removes duplicates).
    * Creates a "content soup" by combining relevant text features (genres, movie_info, directors, actors, etc.).
    * Uses TF-IDF (Term Frequency-Inverse Document Frequency) to vectorize the content soup.
    * Calculates a cosine similarity matrix between all movies.
    * Saves the similarity matrix (`cosine_sim_matrix.npy`), an indexed movie DataFrame (`movies_df_indexed.parquet`), and a title-to-index mapping (`title_to_indices.joblib`).
2.  **Recommendation Logic (`recommender_logic.py`)**:
    * Loads the precomputed artifacts (`.npy`, `.parquet`, `.joblib`).
    * Takes a user-input movie title.
    * Finds the movie in the dataset (with case-insensitive and partial matching).
    * Uses the cosine similarity matrix to find the most similar movies.
3.  **Streamlit Application (`streamlit_app.py`)**:
    * Provides a user interface to enter a movie title and select the number of recommendations.
    * Calls the recommendation logic to display the results.

## Setup and Running

**Prerequisites:**

* Python 3.7+
* Git

**Steps:**

1.  **Clone the repository (or create your local project folder with these files):**
    ```bash
    # If you've pushed to GitHub:
    # git clone [https://github.com/TRISHA16-design/hello-world.git](https://github.com/TRISHA16-design/hello-world.git)
    # cd hello-world
    ```

2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install dependencies:**
    Make sure you have the `requirements.txt` file from the artifact `requirements_file`.
    ```bash
    pip install -r requirements.txt
    ```

4.  **Run the preprocessing script (only needs to be done once, or if the data changes):**
    Ensure your `rotten_tomatoes_movies.csv` and `rotten_tomatoes_movie_reviews-1.csv` are in a `data/` subfolder.
    ```bash
    python preprocess_data.py
    ```
    This will generate:
    * `cosine_sim_matrix.npy`
    * `movies_df_indexed.parquet`
    * `title_to_indices.joblib`

5.  **Run the Streamlit application:**
    ```bash
    streamlit run streamlit_app.py
    ```
    Open your browser and go to the local URL provided by Streamlit (usually `http://localhost:8501`).

## Deployment

This app can be deployed to [Streamlit Community Cloud](https://share.streamlit.io/) for free.
1.  Push all project files (including the generated `.npy`, `.parquet`, `.joblib` artifacts and the `data/` folder) to a public GitHub repository.
2.  Sign up/log in to Streamlit Community Cloud and link your GitHub account.
3.  Deploy the app by selecting your repository and the `streamlit_app.py` file.

## Files Provided

* **`data/rotten_tomatoes_movies.csv`**: Dataset containing movie metadata.
* **`data/rotten_tomatoes_movie_reviews-1.csv`**: Dataset containing movie reviews (not directly used in the current content-based recommender but included for completeness).
* **`streamlit_app.py`**: The main application script. (See artifact `streamlit_app_script`)
* **`recommender_logic.py`**: Contains the core logic for generating recommendations. (See artifact `recommender_logic_script`)
* **`preprocess_data.py`**: Script for data preprocessing and artifact generation. (See artifact `preprocess_script`)
* **`requirements.txt`**: Lists all Python package dependencies. (See artifact `requirements_file`)
* **`movie_recomender.ipynb`**: (Optional) The original Jupyter Notebook used for development and experimentation.
