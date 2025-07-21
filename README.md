# book-harmony-api

# 📚 Book Harmony API

Welcome to the backend service of **Book Harmony** — a personalized book recommendation and journaling platform designed to help readers track, reflect, and grow through their reading journey.

---

## Tech Stack

- **Backend Framework:** Django REST Framework (DRF)
- **Language:** Python 3.11+
- **Database:** SQL lite
- **ORM:** Django ORM
- **Authentication:** Token-based (with plans for OAuth2/Google login in the future)
- **Deployment:** [To be determined: likely Heroku, Render, or AWS EC2]
- **Environment Management:** `.env` using `python-decouple` or `django-environ`

---

## Entity Relationship Diagram (ERD)

```mermaid
erDiagram
    User ||--o{ Library : owns
    User ||--o{ Reflection : writes
    Book ||--o{ Library : stored_in
    Book ||--o{ MoodTag : tagged_with
    Book ||--o{ Reflection : source
    Genre ||--o{ Book : classifies
    MoodTag ||--o{ Reflection : associated_with
    Recommendation ||--|| User : personalized_for
    Recommendation ||--|| Book : recommends

    User {
        UUID id PK
        string username
        string email
        string password
    }

    Book {
        UUID id PK
        string title
        string author
        text description
        UUID genre_id FK
    }

    Library {
        UUID id PK
        UUID user_id FK
        UUID book_id FK
        bool is_favorite
        string status ("read", "reading", "wishlist")
        datetime added_on
    }

    Reflection {
        UUID id PK
        UUID user_id FK
        UUID book_id FK
        text content
        datetime timestamp
    }

    Genre {
        UUID id PK
        string name
    }

    MoodTag {
        UUID id PK
        string label
    }

    Recommendation {
        UUID id PK
        UUID user_id FK
        UUID book_id FK
        float confidence_score
        text algorithm_notes
    }
