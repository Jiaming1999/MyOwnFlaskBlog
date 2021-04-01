# API with flask

## 1. Make a app.py file
What I do firstly to create api is to creating an app.py file (or call it api.py if you prefer it). Inside the app.py file is where you set up for flask server.

```py
from flask import Flask, render_template
from flask_mysqldb import MySQL #This is tool to connect to mySql database

app = Flask(__name__)

@app.route('/')
def home():
    cur = mysql.connection.cursor() # open the cursor
    cur.execute("SELECT username FROM Project.User") #your query goes here
    fetchdata = cur.fetchall() #fetch the data
    cur.close() #close the cursor
    return render_template('home.html', data=fetchdata) #render the page

if __name__ == '__main__':
    app.run(debug=True)

```
Above is a basic template for how app.py file should be. 

And the specific way of creating 4 routes of api (get/put/post/delete) should be:
Example only:

### GET
```py
@app.route('/table', methods=['GET'])
def get():
    # your logical code here
    return # page or data
```

### PUT
```py
@app.route('/table', methods=['PUT'])
def put():
    # your logical code here
    return # page or status
```

### POST
```py
@app.route('/table', methods=['POST'])
def post():
    # your logical code here
    return # page or status
```

### DELETE
```py
@app.route('/table', methods=['DELETE'])
def post():
    # your logical code here
    return # page or status
```
In the above example template code, we use methods=[] to specify what we want to do (CRUD) with our database.

### CORS problem
if ecountering with cors issues, following code could be helpful:
```py
@app.after_request
def after_request(response):
    """
    @https://github.com/corydolphin/flask-cors/issues/200
    To solve connection blocked by cors
    :param response:
    :return:
    """
    response.headers.add('Access-Control-Allow-Origin', 'http://localhost:3000')
    response.headers.add('Access-Control-Allow-Headers', 'Content-Type,Authorization')
    response.headers.add('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE,OPTIONS')
    response.headers.add('Access-Control-Allow-Credentials', 'true')
    return response
```

## 2. The usage of our REST api
After completing the api, next question would be how do we actually use it:
(Following example is shown with javascript file)

How to get 
