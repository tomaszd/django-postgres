# Compose and Django
skeleton for django + docker compose
more info:
https://docs.docker.com/compose/django/
https://stackoverflow.com/questions/23215581/unable-to-perform-collectstatic
Basic setup to have initial django + postgresql dockerized
```
version: "3.9"
   
services:
  db:
    image: postgres
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    depends_on:
      - db
```


Automatic migrations are seto to OFF
to make migrations:
docker exec -t -i <web_container_id> bash
```
echo "Collect static files"
python manage.py collectstatic --noinput

# Apply database migrations
echo "Apply database migrations"
python manage.py migrate

# Start server
echo "Starting server"
python manage.py runserver 0.0.0.0:8000
```

