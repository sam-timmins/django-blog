# Set-up

1. Install django and gnuicorn
```
pip3 install django gunicorn
```

2. Install PostgreSQL and psycopg2
```
pip3 install dj_database_url psycopg2
```

3. Install Cloudinary
```
pip3 install dj3-cloudinary-storage
```

4. Create the requirements.txt file
```
pip3 -freeze --local > requirements.txt
```

5. Create the Django project
```
django-admin startproject ____THE PROJECT NAME____ .
```

### **STEPS 6 TO 8 MUST BE REPEATED EVERYTIME A NEW APP WITHIN THE PROJECT IS CREATED**

6. Create an App within the prtoject
```
python3 manage.py startapp __APP NAME__
```

7. Add the App to the list of installed apps in the project's ````settings.py```` file

```py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'THE NEW APP NAME GOES HERE',
]
```

8. Migrate the changes to the database
```
python3 manage.py migrate
```

9. Check to see the basic project is running
```
python3 manage.py runserver
```

# Link to Heroku for Deployment

1. Navigate to the app from [heroku.com](www.heroku.com) and open the 'Resources' tab.
1. Search for 'Heroku Postgres', select it and click 'submit Order'
1. Check it is there by going to the 'Settings' tab and in the config vars, the  DATABASE_URL should be there.
1. Copy the the URL
1. Within the same directory as the ```manage.py``` file create a ```env.py``` file
1. Ensure the ```env.py``` is in the *.gitignore* file.
1. Generate a SECRET_KEY from [here](https://miniwebtool.com/django-secret-key-generator/)
1. In the ```env.py``` file
    ```py
    import os

    os.environ['DATABASE_URL'] = "URL FORM HEROKU GOES HERE"
    os.environ['SECRET_KEY'] = "GENERATED SECRET KEY GOES HERE"

    ```
1. Navigate to Heroku and the app, within the Config Vars add 
    * KEY = SECRET_KEY
    * VALUE = The generated one that is now in the ```env.py``` file
1. Navigate back to the ```settings.py``` file
```py
import os
import dj_database_url
if os.path.isfile('env.py'):
    import env


# Change the secret key
SECRET_KEY = os.environ.get('SECRET_KEY')


# Change the database

# DATABASES = {
#     'default': {
#         'ENGINE': 'django.db.backends.sqlite3',
#         'NAME': BASE_DIR / 'db.sqlite3',
#     }
# }

DATABASES = {
    'default': dj_database_url.parse(os.environ.get('DATABASE_URL'))
}
```

# Link to Cloudinary
