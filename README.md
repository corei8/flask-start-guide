## ⚠️ WARNING!!

#### This is very much a work in progress and should not be entirely trusted for the time being.

#### There are steps missing, some half-finished code, maybe an _eror_ or _too_.

### 1. Enter your project directory.

```zsh
$ cd project
```

Of course, your project name will be different from mine, but throughout this guide I will use ```project``` anytime I am referring to the project root.

### 2. Create a virtual environment for your project.

```zsh
$ python -m venv env
```

```env``` is what I usually use, but you can choose whatever name you want or need. Throughout this guide, ```env``` will be used as the virtual environment.

### 2. Install Flask and SQLAlchemy

```zsh
$ source env/bin/activate
$ pip install flask
$ pip install -U Flask-SQLAlchemy
```

### 3. Make a simple application.

Make a file and name it the name of your project, just to keep things easy. In thi guide, I am naming my main file ```project.py```. Open it and write: 

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:////tmp/test.db'
# set the following to True if you want, but will be False by default in the future
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
db = SQLAlchemy(app)


class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)

    def __repr__(self):
        return '<User %r>' % self.username
```

### 4. Build the databases

While still in the ```project``` directory:

```bash
$ python
>>> from project import db  # import the database object
>>> db.create_all()         # create the database
>>> quit()                 # exit the python shell
```

This procedure is quite important and you will have to do this many times throughout your project. Everytime you have to rebuild your databases or add a new one, you have to rebuild. If you are having issues with data not being in a database, then this is the first thing you should check.

## Larger Applications

You will want to make your project a package, which will make your life easier as the project gets larger.

You can run you application with:

```bash
flask --app project run
```

