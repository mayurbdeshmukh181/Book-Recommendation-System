# 📚 Book Recommendation System

A collaborative filtering-based book recommendation system that suggests similar books based on user ratings and reading patterns. The system uses cosine similarity to identify books with comparable preferences across users.

## 🎯 Features

- **Intelligent Filtering**: Recommends books based on active readers (200+ ratings) and popular titles (50+ ratings)
- **Collaborative Filtering**: Uses user behavior patterns to find similar books
- **Fast Recommendations**: Pre-computed similarity matrix for instant suggestions
- **Rich Metadata**: Returns book title, author, and cover image for each recommendation
- **Persistent Models**: Serialized models for quick deployment

## 🛠️ Technologies Used

- **Python 3.x**
- **Pandas** - Data manipulation and analysis
- **NumPy** - Numerical computations
- **Scikit-learn** - Cosine similarity calculation
- **Pickle** - Model serialization

## 📋 Prerequisites
```bash
pip install pandas numpy scikit-learn
```

## 🚀 Installation

1. Clone the repository
```bash
git clone https://github.com/yourusername/book-recommendation-system.git
cd book-recommendation-system
```

2. Install required packages
```bash
pip install -r requirements.txt
```

3. Run the notebook or script to generate the models
```bash
python book_recommender.py
```

## 💻 Usage

### Training the Model
```python
# Filter active users (200+ ratings)
x = ratings_with_name.groupby('User-ID').count()['Book-Rating'] > 200
padhle_likheusers = x[x].index

# Filter ratings from active users
filtered_rating = ratings_with_name[ratings_with_name['User-ID'].isin(padhle_likheusers)]

# Filter popular books (50+ ratings)
y = filtered_rating.groupby('Book-Title').count()['Book-Rating'] >= 50
famous_books = y[y].index

# Create final filtered dataset
final_rating = filtered_rating[filtered_rating['Book-Title'].isin(famous_books)]

# Create pivot table
pt = final_rating.pivot_table(index='Book-Title', columns='User-ID', values='Book-Rating')
pt.fillna(0, inplace=True)

# Calculate cosine similarity
from sklearn.metrics.pairwise import cosine_similarity
similarity_score = cosine_similarity(pt)
```

### Getting Recommendations
```python
def recommend(book_name):
    # Fetch book index
    index = np.where(pt.index == book_name)[0][0]
    
    # Get similar items
    similar_items = sorted(list(enumerate(similarity_score[index])), 
                          key=lambda x: x[1], reverse=True)[1:6]
    
    data = []
    for i in similar_items:
        item = []
        temp_df = books[books['Book-Title'] == pt.index[i[0]]]
        item.extend(list(temp_df.drop_duplicates('Book-Title')['Book-Title'].values))
        item.extend(list(temp_df.drop_duplicates('Book-Title')['Book-Author'].values))
        item.extend(list(temp_df.drop_duplicates('Book-Title')['Image-URL-M'].values))
        data.append(item)
    
    return data

# Example usage
recommendations = recommend('Message in a Bottle')
print(recommendations)
```

### Example Output
```python
[
    ['Nights in Rodanthe', 'Nicholas Sparks', 'http://images.amazon.com/...'],
    ['The Mulberry Tree', 'Jude Deveraux', 'http://images.amazon.com/...'],
    ['A Walk to Remember', 'Nicholas Sparks', 'http://images.amazon.com/...'],
    ["River's End", 'Nora Roberts', 'http://images.amazon.com/...'],
    ['Nightmares & Dreamscapes', 'Stephen King', 'http://images.amazon.com/...']
]
```

## 📁 Project Structure
```
book-recommendation-system/
│
├── data/
│   ├── books.csv
│   ├── ratings.csv
│   └── users.csv
│
├── models/
│   ├── pt.pkl              # Pivot table
│   ├── books.pkl           # Books metadata
│   └── similarl.pkl        # Similarity scores matrix
│
├── notebooks/
│   └── book_recommender.ipynb
│
│
├── requirements.txt
├── README.md
└── .gitignore
```

## 📊 How It Works

1. **Data Filtering**: 
   - Selects users with 200+ ratings (active readers)
   - Filters books with 50+ ratings (popular books)
   - Ensures quality recommendations based on substantial data

2. **Feature Engineering**:
   - Creates a user-book rating matrix using pivot table
   - Handles missing values by filling with zeros

3. **Similarity Calculation**:
   - Computes cosine similarity between book vectors
   - Generates a 706×706 similarity matrix

4. **Recommendation Generation**:
   - Finds the top 5 most similar books based on cosine similarity
   - Returns book details with metadata

## 🎓 Algorithm

The system uses **Collaborative Filtering** with **Cosine Similarity**:

- Measures the cosine of the angle between rating vectors
- Books with similar rating patterns across users are considered similar
- Formula: `similarity = cos(θ) = (A·B) / (||A|| ||B||)`

## 📈 Model Performance

- **Matrix Dimensions**: 706 books × filtered users
- **Coverage**: Books with 50+ ratings
- **User Base**: Active readers with 200+ ratings
- **Recommendation Speed**: Instant (pre-computed similarities)

## 🔮 Future Enhancements

- [ ] Add content-based filtering using book descriptions
- [ ] Implement hybrid recommendation system
- [ ] Add user authentication and personalized recommendations
- [ ] Include book genre-based filtering
- [ ] Implement deep learning models (Neural Collaborative Filtering)

## 📝 Dataset

This project uses the [Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset?resource=download) which contains:
- 278,858 users
- 242,135 books
- 1,140,556 ratings

## 👤 Author

**Your Name**
- LinkedIn: [Mayur Deshmukh](https://www.linkedin.com/in/mayur-balasaheb-deshmukh-21145b25a/)

## 🙏 Acknowledgments

- Book-Crossing Dataset creators
- Scikit-learn community
- All contributors and supporters

## 📧 Contact

For any queries, reach out at: your.email@example.com

---

⭐ If you found this project helpful, please give it a star!
