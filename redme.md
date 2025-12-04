commands used
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
# gmail_send/settings.py


urls import views and functions from app2

Rabbit MQ commands:

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



