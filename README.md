# Spotify & YouTube Music Data: Exploratory Data Analysis

## Project Overview

This project performs an in-depth exploratory data analysis (EDA) on a dataset combining Spotify song audio features (like Danceability, Energy, Acousticness) with YouTube video statistics (Views, Likes, Comments) for a collection of tracks. The goal is to uncover relationships between song characteristics, cross-platform popularity, and trends.

## Dataset

The dataset used is `Spotify_Youtube.csv`(Spotify_Youtube.csv) which can be found in this repo or [Kaggle](https://www.kaggle.com/datasets/salvatorerastelli/spotify-and-youtube/data)
*   **Contents:** Contains track information, artist, album details, Spotify audio features, YouTube video URLs, and YouTube video statistics.

## Methodology

1.  **Setup:** Imported necessary libraries and defined constants.
2.  **Loading:** Loaded the dataset using Pandas with robust error handling.
3.  **Cleaning & Preprocessing:**
    *   Corrected data types (e.g., Views, Likes to numeric).
    *   Parsed release dates into datetime objects.
    *   Handled duplicate entries.
    *   Analyzed missing data patterns using `missingno`.
    *   Applied a strategy for handling NaNs (dropping rows with critical missing info, potential for imputation discussed).
4.  **Feature Engineering:**
    *   Extracted `Release_Year` and `Release_Month` from dates.
    *   Created a `Popularity_Score` based on scaled Views, Likes, and Streams.
5.  **Exploratory Data Analysis & Visualization (using Plotly):**
    *   Analyzed distributions of numerical and categorical features.
    *   Investigated correlations (Pearson & Spearman heatmaps).
    *   Examined key relationships using interactive scatter plots.
    *   Compared feature distributions across different groups (e.g., Album Type, Official Video status) using box/violin plots and statistical tests (T-test/ANOVA).
    *   Analyzed trends of features over time.
    *   Generated Word Clouds from track titles after text cleaning.
6.  **Clustering:** Applied KMeans clustering on scaled audio features to identify distinct song profiles and analyzed their characteristics.
7.  **Conclusion:** Summarized key findings, limitations, and potential future work.

## Key Findings from Exploratory Data Analysis

This section outlines the primary observations derived from the visual exploration of the Spotify/YouTube dataset. The analysis focuses on dataset composition, popularity metrics, sonic characteristics, inter-variable relationships, and textual features.

**1. Dataset Composition & Structure**

*   The dataset predominantly features tracks formally released through albums (~70% 'album' type), marked as `Licensed` (68.2%), and having an `official_video` (75.9%). This suggests the analysis is most representative of officially released album tracks.
    *   *Visuals:* [Album Type Distribution](visuals/album_type_distribution.png), [Licensed & Official Video Pie](visuals\licensed_content_distribution.png), [Categorical Frequencies](visuals/categorical_frequencies.png)
*   A small but consistent fraction (2.3%) is categorized as 'Non-Youtube', requiring further investigation to determine if it represents data gaps or platform exclusivity within this dataset.
    *   *Visuals:* [Licensed & Official Video Content Pie](visuals/licensed_content_distribution.png)

**2. Popularity Metrics: Magnitude & Skewness**

*   Popularity metrics (`Views`, `Likes`, `Comments`, `Stream`) exhibit extreme positive skewness. A small number of "superstar" tracks achieve engagement levels orders of magnitude higher than the median track.
    *   *Visuals:* [Top 10 Spotify Songs](visuals/top_10_spotify_songs.png), [Top 10 YouTube Songs](visuals/top_10_youtube_songs.png), [Top 10 YouTube Channels](visuals/top_10_channels.png)
*   Box plots and histograms for these metrics are heavily compressed near zero with numerous extreme outliers, confirming the skewness. This necessitates careful analytical treatment, such as log transformations or non-parametric methods, as standard averages are non-representative.
    *   *Visuals:* [Views Distribution](visuals/hist_Views.png), [Streams Distribution](visuals/hist_Stream.png), [Likes Distribution](visuals/hist_Likes.png), [Comments Distribution](visuals/hist_Comments.png), [Views Box Plot](visuals/hist_Views.png), [Streams Box Plot](visuals/boxplot_Stream.png), [Likes Box Plot](visuals/boxplot_Likes.png), [Comments Box Plot](visuals/boxplot_Comments.png)

**3. Sonic Characteristics: Audio Feature Profiles**

*   The dataset's average sonic profile leans towards higher `Energy`, `Danceability`, and `Loudness`, while `Acousticness`, `Instrumentalness`, and `Speechiness` are strongly skewed towards zero, indicating a prevalence of energetic, vocal-centric music. `Tempo` shows a common bimodal distribution.
    *   *Visuals:* [Energy Distribution](visuals/hist_Energy.png), [Danceability Distribution](visuals/hist_Danceability.png), [Loudness Distribution](visuals/hist_Loudness.png), [Acousticness Distribution](visuals/hist_Acousticness.png), [Instrumentalness Distribution](visuals/hist_Instrumentalness.png), [Speechiness Distribution](visuals/hist_Speechiness.png), [Tempo Distribution](visuals/hist_Tempo.png), [Valence Distribution](visuals/hist_Valence.png)
*   Correlation analysis confirms expected audio relationships (e.g., Energy/Loudness positive, Energy/Acousticness negative). Crucially, correlations between individual audio features and popularity metrics (`Views`, `Stream`) are generally weak (Spearman coefficients mostly between -0.2 and +0.2).
    *   *Visuals:* [Spearman Correlation Matrix](visuals/spearman_correlation_matrix.png), [Pearson Correlation Matrix](visuals/pearson_correlation_matrix.png)
*   This suggests that while tracks adhere to certain sonic norms, individual audio features are not strong standalone predictors of track popularity in this dataset.

**4. Inter-Variable Relationships & Content Format**

*   A significant positive association (Spearman ~0.6) exists between `Spotify Streams` and `YouTube Views`, confirming cross-platform popularity linkage. However, considerable variance around the trend indicates the relationship isn't perfectly linear.
    *   *Visuals:* [Spotify Streams vs YouTube Views Scatter](visuals/scatter_duration_views.png)
*   Song `Duration` shows a non-linear relationship with `YouTube Views`. Extremely long tracks (>20 min) have negligible views, while high view counts concentrate in the standard 2-6 minute range.
    *   *Visuals:* [Song Duration vs YouTube Views Scatter](visuals/scatter_duration_vs_views.png)

**5. Textual Data: Title Characteristics**

*   Track titles are typically concise (distribution peak ~7-8 words).
    *   *Visuals:* [Title Word Count Distribution](visuals/Title%20Word%20Count.png)
*   Word clouds grouped by `Album_type` primarily highlight functional terms ('feat', 'remix', 'live') rather than distinct thematic content, suggesting 'Album Type' is not an effective category for semantic title analysis here.
    *   *Visuals:* [Word Clouds by Album Type](visuals/wordclouds.png)
    
## How to Run

1.  Clone the repository: `git clone <your-repo-url>`
2.  Navigate to the project directory: `cd spotify-youtube-eda`
3.  Download the `Spotify_Youtube.csv` dataset & place it in this directory.
4.  Create a virtual environment (optional but recommended):
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```
5.  Install the required libraries: `pip install -r requirements.txt`
6.  Launch Jupyter Notebook or JupyterLab:
    ```bash
    jupyter notebook
    # or
    jupyter lab
    ```
7.  Open and run the `Spotify_Youtube_Eda.ipynb` notebook.

## Libraries Used

Check [requirements.txt](requirements.txt)

## License

[MIT License](LICENSE.md).