# Adding React with Tailwind CSS to Django Project


## Step 1: Set Up React Inside the Project

1. Create a React app inside the project directory:
   
```bash
# Make sure you're in your project root (django-react-fullstack)
npx create-react-app frontend
```

This will create a frontend directory with all React files.

## 2. Install Tailwind CSS in the React app
```bash
cd frontend
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```


## 3. Configure Tailwind

**Edit frontend/tailwind.config.js:**

```bash
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
    "../templates/**/*.html" // To use Tailwind in Django templates if needed
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

**Edit frontend/src/index.css:**
```bash
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Step 2: Connect Django and React

### 1. Build React for production
```  bash
cd frontend
npm run build
```

This creates a build folder with optimized static files.


### 2. Configure Django to serve React files

**Edit contact_management/settings.py:**


```bash
import os

# Add to TEMPLATES DIRS
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'frontend/build')],  # Add this line
        # ... rest remains same
    }
]

# Add at the bottom
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'frontend/build/static'),
]

```


### 3. Create a Django view to serve React

## Create contact_management/views.py:

```bash
from django.views.generic import TemplateView

class FrontendView(TemplateView):
    template_name = 'index.html'
```



## Update contact_management/urls.py:

```bash
from django.urls import path
from .views import FrontendView

urlpatterns = [
    path('', FrontendView.as_view(), name='home'),
    # ... other URLs
]
```



## Step 3: Create a React Component to Display Contacts

### 1. Install axios for API calls

```bash
cd frontend
npm install axios
```

### 2. Create a Contacts component

  
**Create frontend/src/components/Contacts.js:**

```bash
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function Contacts() {
  const [contacts, setContacts] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const fetchContacts = async () => {
      try {
        const response = await axios.get('/api/contacts/');
        setContacts(response.data);
        setLoading(false);
      } catch (error) {
        console.error('Error fetching contacts:', error);
        setLoading(false);
      }
    };

    fetchContacts();
  }, []);

  if (loading) {
    return <div className="text-center py-8">Loading...</div>;
  }

  return (
    <div className="container mx-auto px-4 py-8">
      <h1 className="text-3xl font-bold mb-6 text-gray-800">Contact Management</h1>
      
      <div className="bg-white shadow-md rounded-lg overflow-hidden">
        <table className="min-w-full divide-y divide-gray-200">
          <thead className="bg-gray-50">
            <tr>
              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Name</th>
              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Email</th>
              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Phone</th>
              <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Address</th>
            </tr>
          </thead>
          <tbody className="bg-white divide-y divide-gray-200">
            {contacts.map((contact) => (
              <tr key={contact.id} className="hover:bg-gray-50">
                <td className="px-6 py-4 whitespace-nowrap">
                  <div className="flex items-center">
                    <div className="ml-4">
                      <div className="text-sm font-medium text-gray-900">
                        {contact.first_name} {contact.last_name}
                      </div>
                    </div>
                  </div>
                </td>
                <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                  {contact.email}
                </td>
                <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                  {contact.phone_number}
                </td>
                <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                  {contact.address}
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
}

export default Contacts;

```

### 3. Update App.js

**Edit frontend/src/App.js:**

```bash
import Contacts from './components/Contacts';

function App() {
  return (
    <div className="App">
      <Contacts />
    </div>
  );
}

export default App;
```


## Step 4: Create Django REST API for Contacts

### 1. Install Django REST Framework

```bash
# Make sure your virtualenv is activated
pip install djangorestframework
```

**Add to INSTALLED_APPS in settings.py:**

```bash
INSTALLED_APPS = [
    # ...
    'rest_framework',
    'contacts',
]
```


### 2. Create a serializer

**Create contacts/serializers.py:**

```bash
from rest_framework import serializers
from .models import Contact

class ContactSerializer(serializers.ModelSerializer):
    class Meta:
        model = Contact
        fields = '__all__'
```


### 3. Create API views

**Update contacts/views.py:**

```bash
from rest_framework import generics
from .models import Contact
from .serializers import ContactSerializer

class ContactListCreate(generics.ListCreateAPIView):
    queryset = Contact.objects.all()
    serializer_class = ContactSerializer
```

### 4. Add API URLs

**Create contacts/urls.py:**

```bash
from django.urls import path
from .views import ContactListCreate

urlpatterns = [
    path('contacts/', ContactListCreate.as_view(), name='contact-list'),
]
```

**Update the main urls.py:**

```bash
from django.urls import path, include

urlpatterns = [
    path('api/', include('contacts.urls')),
    path('', FrontendView.as_view(), name='home'),
]
```


#### Step 5: Run the Full Stack Application

**Start Django backend:**

```bash
python manage.py runserver
```

**In another terminal, start React development server:**

```bash
cd frontend
npm start
```

**Now you can access:**

React frontend: **http://localhost:3000**

Django backend: **http://localhost:8000**

Django admin: **http://localhost:8000/admin**

### Step 6: Create a Production Build (When Ready)

**When you're ready to deploy:**

```bash
cd frontend
npm run build
```

**Django will now serve the production-ready React app at http://localhost:8000**
