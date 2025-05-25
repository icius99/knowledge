---
tags:
  - resource
Area:
---
# Raspberry Pi Django + MySQL Setup Guide (Minimal Install)

  

**Target:** Raspberry Pi 4 (8GB RAM recommended)  

**OS:** Raspberry Pi OS Lite (64-bit)  

**Use case:** Hosting a local inventory app using Django and MySQL

  

---

  

## 1. Flash and Configure Raspberry Pi OS

  

- Download **Raspberry Pi OS Lite (64-bit)** from the [official site](https://www.raspberrypi.com/software/operating-systems/).

- Flash to SD card using [Raspberry Pi Imager](https://www.raspberrypi.com/software/).

- Enable SSH:

  - After flashing, open the SD card and add an empty file named `ssh` (no extension) to the `/boot` directory.

- *(Optional)* Add `wpa_supplicant.conf` to `/boot` to pre-configure Wi-Fi.

  

---

  

## 2. Initial Login and Updates

  

```bash

ssh pi@raspberrypi.local  # default user: pi, password: raspberry

sudo apt update && sudo apt upgrade -y

```

  

*(Optional but recommended)*

  

```bash

sudo raspi-config

# Set hostname, locale, timezone, enable SSH if not done, etc.

```

  

---

  

## 3. Install MySQL Server

  

```bash

sudo apt install -y mariadb-server

sudo mysql_secure_installation

```

  

**Inside the secure setup:**

  

- Set a root password  

- Remove anonymous users  

- Disallow remote root login  

- Remove test database  

  

**Test login:**

  

```bash

sudo mysql -u root -p

```

  

---

  

## 4. Install Python + Dependencies

  

```bash

sudo apt install -y python3 python3-pip python3-venv libmariadb-dev

```

  

**Create and activate a virtual environment:**

  

```bash

mkdir ~/myproject && cd ~/myproject

python3 -m venv venv

source venv/bin/activate

```

  

**Install Django and MySQL support:**

  

```bash

pip install django mysqlclient

```

  

---

  

## 5. Configure Django with MySQL

  

**Create a Django project:**

  

```bash

django-admin startproject inventoryapp .

```

  

**Update `inventoryapp/settings.py`:**

  

```python

DATABASES = {

    'default': {

        'ENGINE': 'django.db.backends.mysql',

        'NAME': 'yourdbname',

        'USER': 'youruser',

        'PASSWORD': 'yourpassword',

        'HOST': 'localhost',

        'PORT': '3306',

    }

}

```

  

**Create the DB in MySQL:**

  

```sql

CREATE DATABASE yourdbname;

CREATE USER 'youruser'@'localhost' IDENTIFIED BY 'yourpassword';

GRANT ALL PRIVILEGES ON yourdbname.* TO 'youruser'@'localhost';

FLUSH PRIVILEGES;

```

  

---

  

## 6. Run the Django App

  

**Apply migrations and run dev server:**

  

```bash

python manage.py migrate

python manage.py runserver 0.0.0.0:8000

```

  

**Access from browser:**

  

```

http://raspberrypi.local:8000

```

  

---

  

## 7. (Optional) Autostart Script on Boot

  

Create a systemd service to run the app automatically if desired. Let me know if you want that added.

  

---

  

**Next Steps:**  

Let me know when you're ready to move beyond the minimal setup — e.g., adding Nginx, Gunicorn, HTTPS, or remote admin tools.