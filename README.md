![Clever Cloud logo](/github-assets/clever-cloud-logo.png)

# Python 3.9 Django Daphne Example on Clever Cloud
[![Clever Cloud - PaaS](https://img.shields.io/badge/Clever%20Cloud-PaaS-orange)](https://clever-cloud.com)

## Overview
This repository provides a complete guide for deploying a Python 3.9 Django application with Daphne ASGI server on [Clever Cloud](https://clever-cloud.com), a European PaaS provider.

[Django](https://www.djangoproject.com/) is a high-level Python web framework that encourages rapid development and clean, pragmatic design. [Daphne](https://github.com/django/daphne) is an HTTP, HTTP2 and WebSocket protocol server for [ASGI](https://en.wikipedia.org/wiki/Asynchronous_Server_Gateway_Interface) applications, and is the reference server for [Django Channels](https://github.com/django/channels). This example demonstrates a minimal Django application that can be deployed on Clever Cloud using Daphne as the ASGI server.

## Prerequisites
- A [Clever Cloud](https://www.clever-cloud.com/) account
- [Clever Tools CLI](https://github.com/CleverCloud/clever-tools) installed and configured
- Basic familiarity with command line operations
- Basic understanding of Python and [Django](https://www.djangoproject.com/)
- A domain name (optional, but recommended for production use)

## Project Structure
```
├── mysite/                  # Django project directory
│   ├── __init__.py
│   ├── asgi.py              # ASGI configuration for Daphne
│   ├── settings.py          # Django settings
│   ├── urls.py              # URL configuration
│   └── wsgi.py              # WSGI configuration (not used with Daphne)
├── manage.py                # Django management script
├── requirements.txt         # Python dependencies
└── README.md                # This documentation
```

## Deployment Guide

### Before You Begin

Before starting the deployment process, you'll need to decide on:

- Application Name: Choose a unique name for your Django application (e.g., my-django-app)
- Domain Name: Optionally, choose a domain name for your application

You'll use these values throughout the deployment process. In the commands below, replace:

- `<APP_NAME>` with your chosen application name
- `<YOUR_DOMAIN_NAME>` with your domain name (if applicable)

### Using Clever Tools CLI

Follow these steps to deploy your Django application on Clever Cloud using the command line:

```bash
# Step 1: Create a Python application
clever create --type python <APP_NAME>

# Step 2: Add your domain (optional but recommended)
clever domain add <YOUR_DOMAIN_NAME>

# Step 3: Configure environment variables
clever env set CC_PYTHON_BACKEND "daphne"
clever env set CC_PYTHON_MODULE "mysite.asgi:application"
clever env set CC_PYTHON_VERSION "3.9"

# Step 4: Push your code to Clever Cloud
clever deploy
```

## Opening your application in a browser

Once deployed, you can access your application at https://<YOUR_DOMAIN_NAME> or at the Clever Cloud generated domain.

### Environment Variables

The following environment variables are used to configure your Python application on Clever Cloud:

- `CC_PYTHON_BACKEND`: Set to `daphne` to use Daphne as the ASGI server
- `CC_PYTHON_MODULE`: Set to `mysite.asgi:application` to specify the ASGI application object
- `CC_PYTHON_VERSION`: Set to `3.9` to specify the Python version

## Running Locally

To run this application locally for testing:

```
# Install dependencies
pip install -r requirements.txt

# Apply database migrations
python manage.py migrate

# Run the Django development server
python manage.py runserver
```

Your application will be available at [http://127.0.0.1:8000/](http://127.0.0.1:8000/)

To run with Daphne instead of the Django development server:

```
# Install dependencies
pip install -r requirements.txt

# Apply database migrations
python manage.py migrate

# Run with Daphne
daphne mysite.asgi:application
```

## Customizing Your Application

This example provides a minimal Django application. To expand it:

1. Create Django apps: `python manage.py startapp myapp`
2. Add routes in mysite/urls.py and your app's urls.py
3. Create models, views, and templates following Django's MVT architecture
4. Update requirements.txt with additional dependencies

## Troubleshooting

If you encounter issues:

1. Check the application logs: `clever logs`
2. Verify all environment variables are correctly set: `clever env`
3. Ensure your application is running: `clever status`

## Contributing

Contributions to improve this deployment example are welcome! Please feel free to submit pull requests or open issues for any enhancements or bug fixes.

## License

This example is provided under the terms of the MIT license.

## Resources

- [Django Documentation](https://docs.djangoproject.com/)
- [Daphne Documentation](https://github.com/django/daphne)
- [Django Channels Documentation](https://channels.readthedocs.io/)
- [Clever Cloud Documentation for Python](https://www.clever-cloud.com/doc/deploy/application/python/python/)
- [Clever Cloud Console](https://console.clever-cloud.com/)
