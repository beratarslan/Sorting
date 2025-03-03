# 📊 Product & Movie Sorting Analysis

This project focuses on sorting products and movies based on various rating methodologies, incorporating Bayesian Average Rating (BAR), weighted sorting, and hybrid models.

---
## 🚀 Features
### **Product Sorting**
- Sorting by Rating
- Sorting by Comment Count or Purchase Count
- Sorting by a Weighted Combination of Rating, Comments, and Purchases
- Sorting by Bayesian Average Rating (BAR)
- Hybrid Sorting (Combining BAR & Other Factors)

### **IMDB Movie Scoring & Sorting**
- Sorting Movies by Vote Average
- Applying IMDb's Weighted Rating Formula
- Sorting Movies by Bayesian Average Rating (BAR)
- Hybrid Sorting for Better Movie Recommendations

---
## 📂 Dataset
This project uses two datasets:
1. Product Dataset (product_sorting.csv)
   - rating: Product rating score
   - purchase_count: Number of purchases
   - comment_count: Number of comments
   - 1_point to 5_point: Distribution of star ratings

2. Movie Dataset (movies_metadata.csv & imdb_ratings.csv)
   - title: Movie name
   - vote_average: IMDb rating
   - vote_count: Number of votes
   - one to ten: Number of votes given for each rating (1 to 10)

---
## 🛠 Installation & Setup
1. Clone the repository:
   git clone https://github.com/your-repo/product-movie-sorting.git
   cd product-movie-sorting

2. Install dependencies:
   pip install -r requirements.txt

3. Run the analysis:
   python analysis.py

---
## 📊 Methodologies
### 1️⃣ Weighted Sorting Score
Combining rating, comment count, and purchase count for ranking products:
weighted_sorting_score = (comment_count_scaled * 32/100) + (purchase_count_scaled * 26/100) + (rating * 42/100)

### 2️⃣ Bayesian Average Rating (BAR)
A more reliable way to rank products/movies based on the distribution of ratings:
score = first_part - z * math.sqrt((second_part - first_part * first_part) / (N + K + 1))

### 3️⃣ Hybrid Sorting (BAR + Other Factors)
Combining Bayesian Average Rating (BAR) with Weighted Sorting Score (WSS) for a final ranking:
hybrid_score = (bar_score * 60/100) + (wss_score * 40/100)

### 4️⃣ IMDb Weighted Rating
IMDb does not use raw averages but a weighted calculation:
weighted_rating = (v / (v + M) * r) + (M / (v + M) * C)
where:
- r = vote average
- v = vote count
- M = minimum votes required
- C = mean vote across all movies

---
## 📖 Example Usage
from analysis import hybrid_sorting_score
ranked_products = hybrid_sorting_score(df)
print("Top Products:", ranked_products.head(10))

from analysis import weighted_rating
imdb_ranked = weighted_rating(df["vote_average"], df["vote_count"], M, C)
print("Top IMDb Movies:", imdb_ranked.head(10))

---
## 🔧 Dependencies
- Python 3.7+
- pandas
- numpy
- scipy
- scikit-learn
