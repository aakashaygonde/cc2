# Google App Engine (GAE) Practical Guide

## Aim

To create and deploy a simple website on Google App Engine using Flask and Cloud Shell.

---

# STEP 1 — Open Google Cloud Console

Open:

```text
https://console.cloud.google.com
```

Login with your Google account.

---

# STEP 2 — Create New Project

1. Click project dropdown (top navbar)
2. Click:

   ```text
   NEW PROJECT
   ```
3. Enter project name:

   ```text
   GAE-Practical
   ```
4. Click:

   ```text
   CREATE
   ```
# STEP — Enable Required APIs

Before creating the App Engine application, enable the required Google Cloud APIs.

Search:
```text
API & Services
```
Open:

Enabled APIs & Services

Click:
```text
+ ENABLE APIS AND SERVICES
```
Enable these APIs one by one:
```text
App Engine Admin API

Cloud Build API

Artifact Registry API

Cloud Storage API
```
Wait 1–2 minutes after enabling the APIs.

# STEP — Add IAM Roles to Service Account

Sometimes deployment may fail due to permission issues.

To fix this:

Search:
```text
IAM
```
Open:
```text
IAM & Admin → IAM
```
Enable:
```text
Include Google-provided role grants
```
Find the App Engine service account:
```text
PROJECT_ID@appspot.gserviceaccount.com
```
Example:
```text
gae-practical-495516@appspot.gserviceaccount.com
```
Click the edit (pencil) icon beside the service account.

Add these roles:
```text
Storage Admin

Cloud Build Editor

App Engine Admin
```
Click:
```text
SAVE
```
Wait a few minutes for permissions to apply.
---

# STEP 3 — Enable App Engine

Search:

```text
App Engine
```

Open App Engine.

Click:

```text
Create Application
```

Choose region:

```text
asia-south1
```

---

# STEP 4 — Open Cloud Shell

Click Cloud Shell icon at top-right:

```text
>_
```

Wait for terminal to start.

---

# STEP 5 — Create Project Folder

```bash
mkdir mywebsite
cd mywebsite
```

---

# STEP 6 — Create `main.py`

```bash
nano main.py
```

Paste:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')
```

Save:

* CTRL + O
* ENTER
* CTRL + X

---

# STEP 7 — Create `requirements.txt`

```bash
nano requirements.txt
```

Paste:

```text
Flask
gunicorn
```

Save and exit.

---

# STEP 8 — Create `app.yaml`

```bash
nano app.yaml
```

Paste:

```yaml
runtime: python312

entrypoint: gunicorn -b :$PORT main:app
```

Save and exit.

---

# STEP 9 — Create Templates Folder

IMPORTANT:
Folder name MUST be:

```text
templates
```

Create folder:

```bash
mkdir templates
```

---

# STEP 10 — Create `index.html`

```bash
nano templates/index.html
```

Paste:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Google App Engine Website</title>

    <style>
        body {
            font-family: Arial;
            background-color: #f4f4f4;
            text-align: center;
            padding-top: 100px;
        }

        .box {
            background: white;
            width: 60%;
            margin: auto;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px gray;
        }

        h1 {
            color: #333;
        }

        p {
            font-size: 18px;
        }
    </style>
</head>

<body>

    <div class="box">
        <h1>Google App Engine Website</h1>

        <p>
            Website successfully deployed on Google App Engine.
        </p>

        <p>
            Cloud Computing Practical Exam
        </p>
    </div>

</body>
</html>
```

Save and exit.

---

# STEP 11 — Check Files

Run:

```bash
ls
```

Output should contain:

```text
app.yaml
main.py
requirements.txt
templates
```

Now verify templates folder:

```bash
ls templates
```

Output:

```text
index.html
```

---

# STEP 12 — Deploy Website

Run:

```bash
gcloud app deploy
```

When asked:

```text
Do you want to continue (Y/N)?
```

Type:

```text
Y
```

Wait for deployment to complete.

---

# STEP 13 — Open Website

```bash
gcloud app browse
```

Website should open successfully.

---

# Important Folder Structure

```text
mywebsite/
│
├── app.yaml
├── main.py
├── requirements.txt
│
└── templates/
    └── index.html
```

---

# Important Files Explanation

| File                   | Purpose           |
| ---------------------- | ----------------- |
| `main.py`              | Flask backend     |
| `requirements.txt`     | Python libraries  |
| `app.yaml`             | GAE configuration |
| `templates/index.html` | Website page      |

---

# Important Viva Questions

## What is Google App Engine?

Google App Engine is a Platform as a Service (PaaS) provided by Google for developing and hosting web applications.

---

## What is PaaS?

PaaS provides a platform to develop and deploy applications without managing servers manually.

---

## Why is `app.yaml` important?

It tells App Engine:

* runtime
* startup command
* deployment configuration

---

## Why use Flask?

Flask is a lightweight Python web framework used for creating web applications.

---

# Common Errors & Fixes

| Error                 | Solution                          |
| --------------------- | --------------------------------- |
| 502 Bad Gateway       | Check `app.yaml` and Flask code   |
| Internal Server Error | Check templates folder            |
| TemplateNotFound      | Ensure folder name is `templates` |
| ModuleNotFoundError   | Check `requirements.txt`          |
| Page not found        | Verify `@app.route('/')`          |

---

# Important Debug Command

View live logs:

```bash
gcloud app logs tail -s default
```

---

# Delete Folder Command

```bash
rm -r foldername
```

Example:

```bash
rm -r templates
```

---

# Rename Folder Command

```bash
mv oldname newname
```

Example:

```bash
mv template templates
```

---

# Final Practical Flow

1. Create project
2. Enable App Engine
3. Open Cloud Shell
4. Create Flask files
5. Create templates folder
6. Deploy using:

   ```bash
   gcloud app deploy
   ```
7. Open using:

   ```bash
   gcloud app browse
   ```

---

# Final Tip

For practical exams:

* Keep project simple
* Focus on successful deployment
* Understand folder structure
* Remember debugging commands

A simple working deployment scores far better than a fancy broken website.
