# Demo Web Application

A simple Python Flask web app used to demonstrate Continuous Deployment with
**Ansible Automation Platform** and **Event-Driven Ansible**.

## Running Locally

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python app.py
# Open http://localhost:8080
```

## Running Tests

```bash
python -m pytest tests/ -v
```

## How Deployment Works

This repo includes a GitHub Actions workflow (`.github/workflows/notify-eda.yml`)
that triggers on every push to `main`:

1. Installs dependencies and runs tests
2. Packages the app as a build artifact
3. Sends a webhook to the EDA Controller

From there, Event-Driven Ansible picks up the event and triggers an Automation
Controller job template that deploys this app to a RHEL 9 server.

## Making Changes for the Demo

Edit the constants at the top of `app.py`:

```python
APP_VERSION = "2.0.0"
APP_TITLE = "Updated Live!"
THEME_COLOR = "#0066cc"
```

Then push:

```bash
git add app.py
git commit -m "v2.0 - live update"
git push
```

The page will update automatically within ~60 seconds.
