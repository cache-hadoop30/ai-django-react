# Mastering React and Django with AI 🚀

**A full-stack learning journey** combining Django (backend) and React (frontend) with **AI-powered mentorship** for accelerated, "vibe coding" experience.

---

## 🌟 Project Philosophy

### **AI-Assisted Learning Framework**
This project is designed to work with AI tools (ChatGPT, Copilot, etc.) using this optimized prompt:

> *"You are an expert mentor in Django (backend) and React (frontend). I am a beginner building full-stack apps. Teach me step-by-step from setting up DRF APIs to connecting them with React+Vite+Tailwind.  
> - Provide clean, beginner-friendly code examples  
> - Explain best practices concisely  
> - Give short exercises after each topic  
> - Maintain a 'vibe coding' approach: fun yet systematic  
> - Encourage hands-on building with mini-tasks  
> - Answer questions with patient mentorship"*

**Key Features:**  
✅ Learn by building real-world projects  
✅ AI explains concepts like a caring mentor  
✅ Progressive difficulty with exercises  
✅ Tailwind CSS for modern styling  

---

## 🛠️ Technical Setup

### **Backend (Django)**
```bash
# 1. Create environment
mkdir myproject && cd myproject
python3 -m venv env  # Linux/Mac
env\Scripts\activate # Windows

# 2. Install dependencies
pip install django djangorestframework

# 3. Initialize project
django-admin startproject backend .
python manage.py startapp api

# 4. Configure settings.py
INSTALLED_APPS = [
    ...,
    'rest_framework',
    'api'
]

# 5. Run server
python manage.py runserver


