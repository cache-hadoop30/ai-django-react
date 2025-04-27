# Day 1: Setup & Basic Django Project

### Pre-requisite
1. Create a project directory (ex. **django-react-fullstack**)
2. Open the folder in Visual Studio Code
3. Open the terminal

---
Let's Start!
   

### 1. Set Up the Django Environment
Before we begin, let's set up a virtual environment to keep our project dependencies isolated.

In the terminal, run the following commands:

```bash
# Install virtualenv if you don’t have it yet
pip install virtualenv

# Create a virtual environment
virtualenv venv


# Activate the virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

Now your environment is set up, and we can move on to installing Django.

![image](https://github.com/user-attachments/assets/dff5ba46-4839-4ba3-ab6c-6a1132966208)


Don't mind the warning. When you see the env folder at the left side panel, it means the env is created.


![image](https://github.com/user-attachments/assets/d7828878-fef1-4efd-9774-697e9abab8a6)



### 2. Install Django
First, you need to install Django. If you haven't installed it yet, use the following command:

```bash
pip install django
```

![image](https://github.com/user-attachments/assets/7d4eb1ba-0256-42b6-a869-af97d0e23aa5)



### 3. Create a Django Project
Now, let’s create a new Django project. In the terminal, navigate to the folder where you want to set up your project and run:

```bash
django-admin startproject contact_management
```

This will create a directory called contact_management with all the necessary files for your Django project.

![image](https://github.com/user-attachments/assets/2aa9eef9-5c54-48a2-8552-bed195a2bcb9)

# Folder Structure
```bash
contact_management/
    manage.py
    contact_management/
        __init__.py
        settings.py
        urls.py
        wsgi.py
        asgi.py
```

![image](https://github.com/user-attachments/assets/2c0f560c-63c8-48c1-806e-437493f0bd88)



### 4. Create a Django App
Now, let’s create an app for managing contacts. In your project directory, run:

```bash
cd contact_management
python manage.py startapp contacts
```
This will create a new folder contacts inside your project directory.


![image](https://github.com/user-attachments/assets/51cc12db-0b8d-4494-89b0-32fab8a76f1a)
        

### 5. Configure the Database
Now, let’s set up the database. By default, Django uses SQLite for development purposes, so you don't need to configure it. You can use the default database settings for now. 

In `settings.py` under the `DATABASES` section, make sure it looks like this:

```bash
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}
```


### 6. Create the Contact Model
Now, let's define the **Contact** model inside the `contacts` app.

Open the `contacts/models.py` file and add the following code to define the Contact model:

```bash
from django.db import models

class Contact(models.Model):
    first_name = models.CharField(max_length=100)
    last_name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
    phone_number = models.CharField(max_length=15)
    address = models.TextField()

    def __str__(self):
        return f"{self.first_name} {self.last_name}"

```

![image](https://github.com/user-attachments/assets/8858a0bb-7019-4924-a0c2-d2e4c0f471d0)


![image](https://github.com/user-attachments/assets/cf1f487b-ffe2-45a4-ac1c-415ca1487ca6)

# Explanation of fields:

- **first_name** and **last_name**: The contact's first and last name.
- **email**: A unique email address for the contact.
- **phone_number**: Contact's phone number (could be validated with regular expressions if needed).
- **address**: A field to store the contact’s address.


![image](https://github.com/user-attachments/assets/67c88117-4f66-492b-8eec-cd8b1e84d9db)


## 7. Register the Model with Admin

Next, let’s register the model in the Django admin interface so that we can manage contacts from the Django admin panel.

In `contacts/admin.py`, add the following code:

```bash
from django.contrib import admin
from .models import Contact

admin.site.register(Contact)
```

This will allow the Contact model to be visible in the Django admin interface.


![image](https://github.com/user-attachments/assets/c828bb5b-8e48-4c3e-831c-2754d06902df)



## 8. Add the App to INSTALLED_APPS

Go to `settings.py` and find the `INSTALLED_APPS` section. Add `'contacts'` to the list of installed apps:

```bash
INSTALLED_APPS = [
    # Other apps...
    'contacts',
]
```

![image](https://github.com/user-attachments/assets/2d9c9481-e6a3-4a62-a888-8d505c37fd57)


## 9. Run Migrations to Create the Database Tables

Now, we need to run migrations to create the database tables based on the model you just created.

```bash
cd contact_management
```

First, let’s make the migrations:

```bash
python manage.py makemigrations contacts
```


Then, apply the migrations:

```bash
python manage.py migrate
```

This will create the Contact table in the SQLite database.

![image](https://github.com/user-attachments/assets/9283b928-bfda-46a3-b760-d5614923a0a3)


## 10. Test the Contact Model with the Admin Panel

Run the development server to make sure everything is set up correctly:

```bash
python manage.py runserver
```


![image](https://github.com/user-attachments/assets/fd58da79-0205-4d6a-be69-6a6883df2cbf)


Now, open your browser and go to http://127.0.0.1:8000/admin/. You'll need to create a superuser if you haven't already:

Open the terminal in Visual Studio Code:

```bash
python manage.py createsuperuser
```

After creating the admin, now run again the server:

```bash
python manage.py runserver
```

Go to http://127.0.0.1:8000/admin/ and login with your credentials.

This is the Dashboard after successfully login.

![image](https://github.com/user-attachments/assets/eefe5008-ca51-46ec-824d-71dfa7baa167)


Follow the prompts to create a superuser account. Once you’ve done that, log in to the admin panel and you should see the Contacts model listed there. You can add, edit, or delete contacts.



---


## Practical Task:
Create the `Contact` model and run `python manage.py makemigrations` to test your model.

## Exercise:
Test the model by running the following commands:

```bash
python manage.py makemigrations
python manage.py migrate
```

### What's Next?
Once Day 1 is complete, you’ll have successfully set up your Django project with the Contact model.

On Day 2, we will move forward by creating a REST API using Django REST Framework (DRF). This will allow us to perform CRUD operations (Create, Read, Update, Delete) on the contacts, providing the backend functionality for your project.


