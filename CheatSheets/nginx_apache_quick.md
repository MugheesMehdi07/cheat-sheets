
## NGINX with Flask/Django

### Without Docker

1. **Install NGINX:**
   ```bash
   sudo apt update
   sudo apt install nginx
   ```

2. **Configure NGINX for Flask/Django:**
   - Create a new configuration file in `/etc/nginx/sites-available/`.
   - Example for Flask:
     ```nginx
     server {
         listen 80;
         server_name your_domain_or_IP;

         location / {
             proxy_pass http://localhost:8000; # Flask runs on 8000
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header X-Forwarded-Proto $scheme;
         }
     }
     ```
   - Enable the file by linking it to the `sites-enabled` directory:
     ```bash
     sudo ln -s /etc/nginx/sites-available/myapp /etc/nginx/sites-enabled
     ```
   - Test NGINX configuration:
     ```bash
     sudo nginx -t
     ```
   - Restart NGINX:
     ```bash
     sudo systemctl restart nginx
     ```

3. **Run Flask/Django app:**
   - Flask:
     ```bash
     flask run --host=0.0.0.0 --port=8000
     ```
   - Django:
     ```bash
     python manage.py runserver 0.0.0.0:8000
     ```

### With Docker

1. **Dockerfile:**
   - Create a `Dockerfile` in your project root.
   - Example for Flask:
     ```Dockerfile
     FROM python:3.8
     COPY . /app
     WORKDIR /app
     RUN pip install -r requirements.txt
     ENTRYPOINT ["python"]
     CMD ["app.py"]
     ```
   - For Django, replace `app.py` with your Django project's WSGI application.

2. **Build and Run the Docker Container:**
   ```bash
   docker build -t myapp .
   docker run -d -p 8000:8000 myapp
   ```

3. **Configure NGINX as a Reverse Proxy (as shown above).**

## Apache with Flask/Django

### Without Docker

1. **Install Apache and mod_wsgi:**
   ```bash
   sudo apt update
   sudo apt install apache2 libapache2-mod-wsgi-py3
   ```

2. **Configure Apache for Flask/Django:**
   - Create a new configuration file in `/etc/apache2/sites-available/`.
   - Example for Flask:
     ```apache
     <VirtualHost *:80>
         ServerName your_domain_or_IP

         WSGIDaemonProcess flaskapp python-path=/path/to/flaskapp
         WSGIScriptAlias / /path/to/flaskapp/flaskapp.wsgi

         <Directory /path/to/flaskapp>
             WSGIProcessGroup flaskapp
             WSGIApplicationGroup %{GLOBAL}
             Require all granted
         </Directory>
     </VirtualHost>
     ```
   - Enable the site:
     ```bash
     sudo a2ensite flaskapp.conf
     ```
   - Restart Apache:
     ```bash
     sudo systemctl restart apache2
     ```

3. **Create a .wsgi file for your Flask/Django app.**
   - Flask (`flaskapp.wsgi`):
     ```python
     from yourapp import app as application
     ```

### With Docker

1. **Dockerfile for Flask/Django (similar to above).**

2. **Build and Run the Docker Container (similar to above).**

3. **Configure Apache as a Reverse Proxy:**
   - Use `ProxyPass` and `ProxyPassReverse` directives in your Apache configuration to pass requests to your Docker container.

