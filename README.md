# Book-Recommendation-System

## Overview
This project implements a collaborative filtering-based book recommendation system that suggests similar books to users based on collective reading patterns and ratings. The system uses cosine similarity to identify books with comparable user preferences.
Methodology
Data Preprocessing
The system begins by filtering the dataset to ensure recommendation quality:

Active User Identification: Selected users who have rated more than 200 books, ensuring recommendations are based on experienced readers with substantial rating histories.
Popular Book Selection: Filtered books that have received at least 50 ratings, focusing on well-known titles with sufficient user feedback to generate reliable similarities.
Data Structuring: Created a pivot table with books as rows and users as columns, with ratings as values. Missing ratings were filled with zeros to create a complete matrix for similarity computation.

Recommendation Engine
Cosine Similarity Approach: The system calculates cosine similarity between book vectors in the user-rating space. This measures the angle between rating patterns, where books with similar rating distributions across users are considered similar.
The resulting similarity matrix (706 × 706) captures relationships between all filtered books in the dataset.
Recommendation Function
The recommend() function takes a book title as input and:

Locates the book's position in the pivot table
Retrieves similarity scores with all other books
Sorts and selects the top 5 most similar books
Returns book details including title, author, and cover image URL

Example Output
For "Message in a Bottle" by Nicholas Sparks, the system recommends:

Other Nicholas Sparks novels (Nights in Rodanthe, A Walk to Remember)
Similar romance/drama authors (Jude Deveraux, Nora Roberts)
Demonstrating the algorithm's ability to identify genre and stylistic similarities

Model Persistence
The system serializes three key components using pickle:

Pivot table (pt.pkl)
Books metadata (books.pkl)
Similarity scores matrix (similarl.pkl)

This enables quick deployment and eliminates the need to recalculate similarities for each recommendation request.
Key Features

Collaborative filtering based on user behavior patterns
Quality-focused: Uses only highly-rated books and active readers
Fast recommendations: Pre-computed similarity scores enable instant suggestions
Rich metadata: Provides book titles, authors, and cover images for enhanced user experience

This system effectively captures reading preferences through collective intelligence, making it suitable for book discovery platforms and reading recommendation services.
