# Developer Skills API

## Overview
The Developer Skills API is a web API built with Python, that allows users to track and manage their skills. The API uses Python with Flask for the backend, and PostgreSQL for the database, which is connected via an internal private network on Render. Both the API and Database are hosted on Render, to allow for this private connection.

Currently this implementation  only has a backend and there is no frontend implementation as of yet. There are plans to add API frontend. [ My Portfolio website](https://jaredmcdowall.me/) has a basic frontend implementation in React.

## API Features
- **POST**: Add new skill
- **GET**: Get all skills
- **DELETE**: Remove a skill
- **PUT**: Decrement the count of a skill 
- **GET**: Get details of a specific skill

## Setup and Installation

### Prerequisites
- Python 3.11
- PostgreSQL
- pip (Python package installer)

There is no local version of this API. This implementation uses a internal private connection, so the database integration will not work unless you change the database connection.

In order to change databse connection go to `main.py` in root directory. Then input your own database address, ensure the databse will allow all connections.

```python
# Entry point of the application
if __name__ == "__main__":
    # Connect to the PostgreSQL database via internal connection on Render
    # Create an instance of the SkillsService class
    db_url = ""
    skills_service = service.SkillsService(PostgreSQLRepository(db_url))
```

This API is bound to `0.0.0.0` for Render, change if needed in `main.py`

```python
 # Start the Flask app
    app.run(debug=False, host='0.0.0.0')
```

### Installation Steps
1. **Clone the repository:**
    ```sh
    git clone https://github.com/yourusername/developer-skills-tracker.git
    cd developer-skills-tracker
    ```

2. **Create a virtual environment and activate it:**
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. **Install the required packages:**
    ```sh
    pip install -r requirements.txt
    ```

4. **Set up the PostgreSQL database:**
    - Create a new PostgreSQL database.
    - Update the `db_url` in `main.py` with your PostgreSQL database connection string.

5. **Run the application:**
    ```sh
    python main.py
    ```

## API Endpoints

### Get All Skills
- **URL:** `/api/skills/get_all_skills`
- **Method:** `GET`
- **Response:**
    ```json
    [
        {
            "skill_name": "Python",
            "count": 5
        },
        ...
    ]
    ```

### Add a Skill
- **URL:** `/api/skills/add_skill/<string:skill_name>`
- **Method:** `POST`
- **Response:**
    - Success: `201 Created`
    - Error: `400 Bad Request` or `403 Forbidden`

### Remove a Skill
- **URL:** `/api/skills/remove_skill/<string:skill_name>`
- **Method:** `PUT`
- **Response:**
    - Success: `204 No Content`
    - Error: `404 Not Found`

### Decrement a Skill
- **URL:** `/api/skills/decrement_skill/<string:skill_name>`
- **Method:** `PUT`
- **Response:**
    - Success: `204 No Content`
    - Error: `404 Not Found`

### Get a Specific Skill
- **URL:** `/api/skills/get_skill/<string:skill_name>`
- **Method:** `GET`
- **Response:**
    - Success: `200 OK`
    - Error: `404 Not Found`