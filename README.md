# pandas-flask-sqlalchemy
Docker base image for Flask apps

The image is available as **markuswb/pandas-flask-sqlalchemy** 
on [Docker Hub](https://hub.docker.com/r/markuswb/pandas-flask-sqlalchemy)

## Usage
Base image for [Flask](https://flask.palletsprojects.com/en/2.1.x/) webapps/APIs with support for login with [JWT](https://itsdangerous.palletsprojects.com/en/2.1.x/),  [SQLAlchemy](https://flask.palletsprojects.com/en/1.1.x/patterns/sqlalchemy/) database connection, numpy and pandas pre-installed. [waitress](https://docs.pylonsproject.org/projects/waitress/en/latest/) ist provided as production server.

Derive your image with a Dockerfile similar to

<pre><code>FROM markuswb/pandas-flask-sqlalchemy

EXPOSE 5000

ENV FLASK_APP myapp.py
ENV FLASK_CONFIG docker

COPY app app
COPY myapp.py config.py boot.sh ./
USER application
CMD ["./boot.sh"]
</code></pre>

The start script `boot.sh` should contain the lines

<pre><code>#!/bin/sh
source venv/bin/activate
exec waitress-serve --port=5000 myapp:app
</code></pre>

to activate the virtual environment and start the web server. For database initialization a deployment script might be necessary.
