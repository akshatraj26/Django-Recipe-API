# Recipe API

A Django-powered API for managing and sharing recipes. The API includes Swagger documentation for ease of use, user authentication, and granular permissions to ensure secure access to endpoints. The project is containerized for easy deployment on any platform and is currently live on PythonAnywhere.

## Features
- **Swagger Integration**: Interactive API documentation at `/api/doc/`.
- **Authentication**: Supports token-based authentication.
- **Permissions**: Role-based access to endpoints (e.g., only authenticated users can create recipes).
- **CRUD Operations**: Endpoints for creating, reading, updating, and deleting recipes.
- **Database Support**:
  - **PostgreSQL**: Used during Dockerizing.
  - **MySQL**: Used during deployment on PythonAnywhere.
- **Containerized**: Ready-to-deploy using Docker.

## Live API

The API is live at: [https://akshatraj26.pythonanywhere.com/api/docs/](https://akshatraj26.pythonanywhere.com/api/docs/)

Use this link to explore the API documentation and interact with the endpoints directly.

## Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- Docker (if using containerization)

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/akshatraj26/Django-Recipe-API.git
   cd Django-Recipe-API
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Configure the database in `settings.py`:
   - Use PostgreSQL for containerized setups.
   - Use MySQL for deployments like PythonAnywhere.

5. Run database migrations:
   ```bash
   python manage.py migrate
   ```

6. Create a superuser to access the admin panel:
   ```bash
   python manage.py createsuperuser
   ```

7. Start the development server:
   ```bash
   python manage.py runserver
   ```

## Authentication and Permissions

- **Authentication**:
  Token-based authentication using Django REST Framework.
  Obtain a token by logging in at `/api/token/`.

- **Permissions**:
  - Authenticated users can perform all CRUD operations on recipes.
  - Specific roles or groups may be configured for finer control.

## Swagger Documentation

The API documentation is available at `/api/doc/` (live version: [here](https://akshatraj26.pythonanywhere.com/api/docs/)). Use it to interact with the API directly from the browser.

## Containerization with Docker

The project includes a `Dockerfile` and `docker-compose.yml` for easy containerization.

### Build and Run the Container

1. Configure the environment variables for PostgreSQL in the `.env` file.

2. Build the Docker image:
   ```bash
   docker build -t recipe-api .
   ```

3. Run the container:
   ```bash
   docker run -p 8000:8000 recipe-api
   ```

4. Access the API at `http://localhost:8000`.

### Docker Compose

If you're deploying with Docker Compose, use the `docker-compose.yml` file:
```bash
docker-compose up
```

This will build and start the container along with PostgreSQL as the database.

## Deployment on PythonAnywhere

1. **Database**:
   - The project uses MySQL on PythonAnywhere. Update the `DATABASES` settings in `settings.py` accordingly.

2. **Static Files**:
   Collect static files before deployment:
   ```bash
   python manage.py collectstatic
   ```

3. **Environment Variables**:
   Store sensitive information (e.g., database credentials, `SECRET_KEY`) in a secure way, like in a `.env` file or directly in PythonAnywhere's settings.

4. **Deployment**:
   Upload the project to PythonAnywhere and follow the [PythonAnywhere Deployment Steps](https://akshatraj26.pythonanywhere.com/api/docs/).

## Usage

Once deployed, the API is accessible at:
- Recipes Endpoint: `/api/recipes/`
- Token Endpoint: `/api/token/`
- Swagger Documentation: `/api/doc/`

For the live version:
- API Documentation: [https://akshatraj26.pythonanywhere.com/api/docs/](https://akshatraj26.pythonanywhere.com/api/docs/)

## License

This project is licensed under the [MIT License](LICENSE).
