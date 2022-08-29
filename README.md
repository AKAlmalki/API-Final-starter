# The Book Shelf of Udacity  - TODO: CHANGE THIS TITLE [done]

This is one of the greatest bookshelves you can find online, which have a lot of books from different categories and fields. A lot of people can read these books and rate it based on their opinion, and an author could publish a book and see what people think of his books through the rating. A student is able to add books, give them rating, update the rating, and search for a book using the title (case-insensitive and partial search).

All backend code follows [PEP8 style guidelines](https://www.python.org/dev/peps/pep-0008/).
## Getting Started

### Prerequisites & Installation

Developers using this project should already have Python3, pip and node installed on their local machines.

#### Backend

- You should have the following requirements packages are included in your `requirements.txt` file :
```
aniso8601==6.0.0
Click==7.0
Flask==1.0.3
Flask-Cors==3.0.7
Flask-RESTful==0.3.7
Flask-SQLAlchemy==2.4.0
itsdangerous==1.1.0
Jinja2==2.10.1
MarkupSafe==1.1.1
psycopg2-binary==2.8.2
pytz==2019.1
six==1.12.0
SQLAlchemy==1.3.4
Werkzeug==0.15.4
```

 - Make sure all the requirements are in the `requirements.txt` file.
 - Use the following command in the terminal (make sure you are in the same directory of the requirements file) from the backend folder.

```
& pip3 install -r requirements.txt
```

- Update Configuration for the DB

  - You should have two databases with the names `bookshelf` and `bookshelf_test` created in your machine.
  - In the `models.py` file, you should change the `database_path` and `database_name` based on your settings of DB.
```bash
database_name = "your_DB_name"
database_path = "postgresql://{}:{}@{}/{}".format(
    "DB_user", "DB_password", "localhost:5432", database_name
)
```
 
- Run your FLASK server

  - In order to run your FLASK server locally, open the terminal and make sure your are in the backend directory for the project, then writer the following command lines to start the server:
```
$ export FLASK_APP=flaskr
$ export FLASK_ENV=development
$ flask run
```
NOTE: make sure there's no additional spaces because that makes problems sometimes.

These above commands put the application in development mode which means that the application will show an interactive debugger in the console and restarts the server whenever there's some changes to the application, look for more in [Flask documentation](https://flask.palletsprojects.com/en/1.0.x/tutorial/factory/)

- How to run Tests

  - In order to run the test we have in our project, you should make sure of the following:
  - the database name should be `bookshelf_test` as it's in your machine.
  - the database path should be updated to your database path by updating the `username` and the `password`.
  - Next, you should open your terminal in the project directory, specifically in the backend folder, then run the following command:
  - `python3 test_flaskr.py`
  - Results should show how many tests passed, and the time taken to run these test (if there's any errors or not passed tests it should be displayed too).
 
 #### SAMPLE: running the test_flaskr.py
 ```bash
 .../backend$ python3 test_flaskr.py
.........
----------------------------------------------------------------------
Ran 9 tests in 0.311s

OK
```
.

#### Frontend

From the frontend folder, run the following commands to start the client:
```
npm install // only once to install dependencies
npm start 
```
By default, the frontend will run on localhost:3000. 


## API Reference

### Getting Started
- Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, `http://127.0.0.1:5000/`, which is set as a proxy in the frontend configuration. 
- Authentication: This version of the application does not require authentication or API keys. 

### Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```
The API will return three error types when requests fail:
- 400: Bad Request
- 404: Resource Not Found
- 422: Not Processable 
- 405: Method Not Allowed

### Endpoints 
#### GET /books
- General:
    - Returns a list of book objects, success value, and total number of books
    - Results are paginated in groups of 8. Include a request argument to choose page number, starting from 1. 
- Sample: `curl http://127.0.0.1:5000/books`

``` {
  "books": [
    {
      "author": "Stephen King",
      "id": 1,
      "rating": 5,
      "title": "The Outsider: A Novel"
    },
    {
      "author": "Lisa Halliday",
      "id": 2,
      "rating": 5,
      "title": "Asymmetry: A Novel"
    },
    {
      "author": "Kristin Hannah",
      "id": 3,
      "rating": 5,
      "title": "The Great Alone"
    },
    {
      "author": "Tara Westover",
      "id": 4,
      "rating": 5,
      "title": "Educated: A Memoir"
    },
    {
      "author": "Jojo Moyes",
      "id": 5,
      "rating": 5,
      "title": "Still Me: A Novel"
    },
    {
      "author": "Leila Slimani",
      "id": 6,
      "rating": 5,
      "title": "Lullaby"
    },
    {
      "author": "Amitava Kumar",
      "id": 7,
      "rating": 5,
      "title": "Immigrant, Montana"
    },
    {
      "author": "Madeline Miller",
      "id": 8,
      "rating": 5,
      "title": "CIRCE"
    }
  ],
"success": true,
"total_books": 18
}
```

#### POST /books
- General:
    - Creates a new book using the submitted title, author and rating. Returns the id of the created book, success value, total books, and book list based on current page number to update the frontend. 
- `curl http://127.0.0.1:5000/books?page=3 -X POST -H "Content-Type: application/json" -d '{"title":"Neverwhere", "author":"Neil Gaiman", "rating":"5"}'`
```
{
  "books": [
    {
      "author": "Neil Gaiman",
      "id": 24,
      "rating": 5,
      "title": "Neverwhere"
    }
  ],
  "created": 24,
  "success": true,
  "total_books": 17
}
```
#### DELETE /books/{book_id}
- General:
    - Deletes the book of the given ID if it exists. Returns the id of the deleted book, success value, total books, and book list based on current page number to update the frontend. 
- `curl -X DELETE http://127.0.0.1:5000/books/16?page=2`
```
{
  "books": [
    {
      "author": "Gina Apostol",
      "id": 9,
      "rating": 5,
      "title": "Insurrecto: A Novel"
    },
    {
      "author": "Tayari Jones",
      "id": 10,
      "rating": 5,
      "title": "An American Marriage"
    },
    {
      "author": "Jordan B. Peterson",
      "id": 11,
      "rating": 5,
      "title": "12 Rules for Life: An Antidote to Chaos"
    },
    {
      "author": "Kiese Laymon",
      "id": 12,
      "rating": 1,
      "title": "Heavy: An American Memoir"
    },
    {
      "author": "Emily Giffin",
      "id": 13,
      "rating": 4,
      "title": "All We Ever Wanted"
    },
    {
      "author": "Jose Andres",
      "id": 14,
      "rating": 4,
      "title": "We Fed an Island"
    },
    {
      "author": "Rachel Kushner",
      "id": 15,
      "rating": 1,
      "title": "The Mars Room"
    }
  ],
  "deleted": 16,
  "success": true,
  "total_books": 15
}
```
#### PATCH /books/{book_id}
- General:
    - If provided, updates the rating of the specified book. Returns the success value and id of the modified book. 
- `curl http://127.0.0.1:5000/books/15 -X PATCH -H "Content-Type: application/json" -d '{"rating":"1"}'`
```
{
  "id": 15,
  "success": true
}
```
