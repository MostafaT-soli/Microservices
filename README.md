# Microservice Documentation

## Overview

This documentation covers the architecture and deployment of a Python-based microservice built using the Flask framework. The application is designed as a containerized microservice, packaged and deployed via docker.

---

## Error Resolution

### Issue #1: Dependency Import Error

#### Description

During the Dockerization of the Flask microservice, an import error occurs, preventing the app from running. The traceback encountered is as follows:

```plaintext
Traceback (most recent call last):
  File "/usr/local/bin/flask", line 5, in <module>
    from flask.cli import main
  File "/usr/local/lib/python3.9/site-packages/flask/__init__.py", line 5, in <module>
    from .app import Flask as Flask
  File "/usr/local/lib/python3.9/site-packages/flask/app.py", line 30, in <module>
    from werkzeug.urls import url_quote
ImportError: cannot import name 'url_quote' from 'werkzeug.urls' (/usr/local/lib/python3.9/site-packages/werkzeug/urls.py)
```

#### Cause

This issue is caused by an incompatibility with the latest version of the Werkzeug library. url_quote, a previously available function, has been removed in recent versions, causing Flask to break when attempting to import this function.
Solution

To resolve this issue, lock the Werkzeug version to 2.2.2 in requirements.txt. This version maintains compatibility with the Flask version used by this application.
Steps to Fix

1. Open `requirements.txt`.
2. Add the following line: `Werkzeug==2.2.2`
