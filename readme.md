# Django + Celery Demo Project

A Django web app with two apps (app1, app2). Users submit reviews via a web form at `/reviews/`, which triggers an async Celery task to send email notifications. Celery workers process tasks in the background using RabbitMQ as the message broker, keeping the web response fast while emails are sent asynchronously.

---

## Commands used
proj/celery_app.py
       │
       ▼
app.autodiscover_tasks()  ──►  Scans INSTALLED_APPS in settings.py
       │
       ▼
┌──────┴──────┐
▼             ▼
app1/tasks.py    app2/tasks.py

commandto start celery:   celery -A proj worker -l info

The Celery worker auto-discovers tasks from app1 and app2. This works because:
1. `app.autodiscover_tasks()` in celery_app.py scans all INSTALLED_APPS for tasks.py files
2. app1 and app2 are listed in settings.py under INSTALLED_APPS: 'app1', 'app2'

all the configs are read from main app (proj) settings.py

### Gmail Setup for Email Sending

1. Create a Gmail account (or use an existing one)
2. Enable 2-Step Verification: [Google Account Security](https://myaccount.google.com/security)
3. Generate an App Password:
   - Go to [App Passwords](https://myaccount.google.com/apppasswords)
   - Select "Mail" and your device
   - Copy the 16-character password
4. Update `proj/settings.py`:
   EMAIL_HOST_USER = 'your-email@gmail.com'
   EMAIL_HOST_PASSWORD = 'xxxx xxxx xxxx xxxx'  # App password (not your Gmail password)
   DEFAULT_FROM_EMAIL = 'your-email@gmail.com'
   
## urls import views from app2

## Rabbit MQ commands:

sudo dnf install rabbitmq-server

sudo dnf install erlang

sudo systemctl enable --now rabbitmq-server

systemctl status rabbitmq-server

sudo rabbitmq-plugins enable rabbitmq_management

sudo systemctl restart rabbitmq-server

http://localhost:15672

sudo rabbitmqctl add_user admin MyPassword123
sudo rabbitmqctl set_user_tags admin administrator
sudo rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"



## start locally:
update email/ app password/ to list in the settings.py

python manage.py runserver

sudo systemctl enable --now rabbitmq-server

celery -A proj worker -l info


