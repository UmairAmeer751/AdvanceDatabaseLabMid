🎬 Movie Streaming Platform Backend

✨ Project Summary

A robust, MongoDB-based backend system designed for a modern movie streaming platform. This application powers core functionality, including content management, user interactions, and sophisticated data retrieval through keyword, fuzzy, semantic, and hybrid search capabilities. It also provides essential analytics using MongoDB's aggregation framework.

🚀 Getting Started

📦 Key Technologies & Dependencies

This project relies on the following key Python libraries:

FastAPI: Core framework for building high-performance RESTful APIs.

Uvicorn: ASGI server to run the FastAPI application.

PyMongo / BSON: Python driver for connecting to and interacting with MongoDB.

python-dotenv: Securely loads environment variables (e.g., MongoDB URI) from a .env file.

sentence-transformers: Generates vector embeddings for advanced semantic search.

scikit-learn: Used for calculating cosine similarity in the hybrid ranking model.

numpy: Essential library for numerical operations and data normalization.

datetime: Handling and filtering data based on timestamps.

⚙️ Core Features

User & Content Management (CRUD): Complete management of movies, users, and reviews.

Watch History Tracking: Records detailed user activity (movie ID, timestamp, duration).

Advanced Search:

Keyword Search: Search by title, director, or cast.

Fuzzy Search: Typo-tolerant matching for more efficient, real-world searches.

Semantic Search: Title similarity search using vector embeddings.

Hybrid Ranking: Combines similarity score with movie rating and popularity for highly relevant results.

Data Analytics: Aggregation queries to derive valuable business insights (e.g., Top 5 most-watched movies, average ratings).

🧠 Database Design & Schema

The system uses four main collections to manage all relational data:

movies

Description: Stores all movie metadata and embedded rating data.

Key Fields: title, description, genres, director, rating, popularity.

Indexing Strategy: Text index (title, director, cast.name), and indexes on genres, rating.average, popularity.

users

Description: Stores user profiles.

Key Fields: name, email, subscription_type.

Indexing Strategy: Unique index on email, index on name.

watchHistory

Description: Logs every instance of a movie being watched by a user.

Key Fields: user_id (reference to users), movie_id (reference to movies), timestamp, watch_duration.

Indexing Strategy: Indexes on movie_id, user_id, timestamp.

reviews

Description: Stores user-submitted ratings and text reviews.

Key Fields: user_id (reference to users), movie_id (reference to movies), rating, review_text.

Indexing Strategy: Indexes on movie_id, user_id, timestamp.

🌐 API Endpoints

The API is structured to provide flexible data access and manipulation.

Search and Retrieval Endpoints

Endpoint: /movies/search

Method: GET

Description: Keyword & Fuzzy Search with typo tolerance across title, director, and cast. Results are ranked by a similarity score (sum of title, cast, director score).

Parameters: query (string)

Endpoint: /movies/title/{title}

Method: GET

Description: Semantic Similarity Search based on the movie title's embedding (typo tolerant).

Parameters: title (path parameter)

Endpoint: /movies/hybrid/{title}

Method: GET

Description: Hybrid Ranking Search that combines semantic title similarity, average rating (normalized), and popularity (normalized) into a final weighted score.

Parameters: title (path parameter)

User and Review Endpoints

Endpoint: /users/{userId}/history

Method: GET

Description: Retrieves a user's complete watch history, joining records with movie details (title, director, etc.) using aggregation pipelines.

Example URL: .../users/68f265966fb4862d984a24a0/history

Endpoint: /movies/{movie_id}/reviews

Method: GET

Description: Fetches all reviews for a specific movie, including user details (name, email) using aggregation.

Example URL: .../movies/68f25b136fb4862d984a2457/reviews

Endpoint: /Movie/addReview

Method: POST

Description: Allows a user to submit a new rating and text review for a movie.

Endpoint: /users/registration

Method: POST

Description: Creates a new user record in the users collection.

Endpoint: /movie/{movie_id}/avgRating

Method: GET

Description: Calculates and returns the current average rating for a given movie.

Analytics Endpoints

Endpoint: /topWatchedMovies

Method: GET

Description: Aggregates and returns the Top 5 most watched movies based on total watches and total watch time.

🛠 Running the Application

Activate Virtual Environment:

D:\CUI LHR\5th Sem\ADB\LAB\movie_streaming_backend-main\.venv\Scripts\activate


Start Uvicorn Server:

uvicorn main:app --reload


Access: The API will be available at http://127.0.0.1:8000.

Documentation: http://127.0.0.1:8000/docs
