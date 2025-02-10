# Django Database Sharding Project

This project demonstrates how to implement **database sharding** in Django using multiple PostgreSQL databases. The application is designed to route database queries (both read and write) to different shards based on the region specified by the user. It uses Django REST Framework to expose an API for creating orders, with data being stored in the appropriate shard (India, USA, Europe) based on the provided region.

## Project Structure

django_databasesharding/
│── django_databasesharding/  # Project root directory
│   ├── __init__.py
│   ├── settings.py           # Django settings (including database sharding config)
│   ├── urls.py               # URL routing
│   ├── wsgi.py               # WSGI application entry point
│   ├── asgi.py               # ASGI application entry point (for async support)
│   ├── manage.py             # Django CLI management script
│
│── app/                      # Application directory
│   ├── __init__.py
│   ├── models.py             # Database models (SaleOrder model defined here)
│   ├── views.py              # API views (SaleOrderCreateView defined here)
│   ├── serializers.py        # Django Rest Framework serializers
│   ├── db_router.py          # Database router logic (GeoShardingRouter)
│   ├── urls.py               # Application-specific URL routing
│   ├── admin.py              # Django admin configurations
│   ├── migrations/           # Database migrations
│   ├── tests.py              # Unit tests for the application
│   ├── apps.py               # App configuration
│
│── requirements.txt          # Project dependencies (Django, DRF, PostgreSQL)
│── README.md                 # Documentation

## Requirements

To run this project, you need

## Installation

1. **Clone the repository:**
    https://github.com/rahulbhu64/django-sharded-database.git


## Install dependencies
pip install -r requirements.txt

## Setup PostgreSQL Databases:

Create three PostgreSQL databases: db_india, db_usa, and db_europe.
Ensure your PostgreSQL server is running and accessible from Django.
Configure Database Credentials:

Update the database credentials in django_databasesharding/settings.py under the DATABASES section to match your local setup.

## Apply Migrations:

# Run the following commands to apply migrations for each database shard:

python manage.py makemigrations app
python manage.py migrate --database=shard_india
python manage.py migrate --database=shard_usa
python manage.py migrate --database=shard_europe

# Run server

python manage.py runserver
