
# Recipe API

A Django-powered RESTful API for managing and sharing recipes. The API includes Swagger documentation for ease of use, secure authentication, and granular permissions. It’s fully containerized using **Docker and PostgreSQL**, making it easy to deploy on any platform — including **AWS EC2** and **PythonAnywhere**.

---

## 🚀 Features

* **Swagger Integration** – Interactive API documentation at `/api/doc/`.
* **Authentication** – Token-based authentication using Django REST Framework.
* **Permissions** – Role-based access; only authenticated users can create, update, or delete recipes.
* **CRUD Operations** – Endpoints for creating, reading, updating, and deleting recipes.
* **Database Support**

  * **PostgreSQL** – Used during Docker containerization and EC2 deployment.
  * **MySQL** – Used for deployment on PythonAnywhere.
* **Containerized** – Fully Dockerized with PostgreSQL service and environment variables.

---

## 🌐 Live API

**Live Demo:** [https://akshatraj26.pythonanywhere.com/api/docs/](https://akshatraj26.pythonanywhere.com/api/docs/)
You can explore and test all API endpoints directly from the Swagger interface.

**Repository:** [GitHub – Django-Recipe-API](https://github.com/akshatraj26/Django-Recipe-API.git)

---

## ⚙️ Prerequisites

* Python 3.8 or higher
* pip (Python package manager)
* Docker and Docker Compose

---

## 🧩 Installation (Local Setup)

1. **Clone the repository:**

   ```bash
   git clone https://github.com/akshatraj26/Django-Recipe-API.git
   cd Django-Recipe-API
   ```

2. **Create and activate a virtual environment:**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure the database in `settings.py`:**

   * Use **PostgreSQL** for Docker/EC2 deployment.
   * Use **MySQL** for PythonAnywhere deployment.

5. **Run migrations and create a superuser:**

   ```bash
   python manage.py migrate
   python manage.py createsuperuser
   ```

6. **Start the development server:**

   ```bash
   python manage.py runserver
   ```

---

## 🔐 Authentication & Permissions

* **Authentication:**
  Token-based authentication using DRF. Obtain a token by posting credentials to `/api/token/`.

* **Permissions:**

  * Authenticated users can perform all CRUD operations.
  * Unauthenticated users have read-only access (if configured).
  * Extendable role-based groups for admin and contributors.

---

## 🧾 Swagger Documentation

Swagger UI available at `/api/doc/`
👉 [Live version here](https://akshatraj26.pythonanywhere.com/api/docs/)

---

## 🐳 Containerization with Docker

This project includes a preconfigured `Dockerfile` and `docker-compose.yml` that build and run both the Django app and the PostgreSQL database.

### Build & Run the Containers

1. Create a `.env` file in your project root:

   ```env
   DB_NAME=recipe
   DB_USER=postgres
   DB_PASSWORD=postgres
   DB_HOST=db
   DB_PORT=5432
   DJANGO_ALLOWED_HOSTS=localhost,127.0.0.1
   ```

2. **Build the Docker image:**

   ```bash
   docker-compose build
   ```

3. **Run the containers:**

   ```bash
   docker-compose up
   ```

4. Access the API locally at:
   [http://localhost:8000/api/docs/](http://localhost:8000/api/docs/)

---

## 🧪 Testing

The project includes unit tests for API reliability and backend integrity.

### ✅ Tests Completed

* **User Authentication**

  * Token generation and validation.
  * Rejection of invalid credentials.

* **Recipe CRUD**

  * Recipe creation, update, deletion, and retrieval.
  * Authenticated vs. unauthenticated user access control.

* **Model Validation**

  * Recipe, Tag, and Ingredient model relationships.
  * String representation and field constraints.

* **Custom Commands**

  * `wait_for_db` tested for PostgreSQL availability before startup.

* **Health Check**

  * Ensures `/api/health/` endpoint responds successfully.

### 🧭 Future Tests

* Integration and performance tests.
* Permission and role-based edge cases.
* Swagger and documentation validation.

### Run Tests

**Using Docker Compose:**

```bash
docker-compose run --rm app sh -c "python manage.py test"
```

**Using Local Environment:**

```bash
python manage.py test
```

---

## 🧰 Useful Docker Commands

| **Command**                                                           | **Description**                           |
| --------------------------------------------------------------------- | ----------------------------------------- |
| `docker-compose run --rm app sh -c "python manage.py makemigrations"` | Create migrations.                        |
| `docker-compose run --rm app sh -c "python manage.py migrate"`        | Apply migrations.                         |
| `docker-compose run --rm app sh -c "python manage.py test"`           | Run test suite.                           |
| `docker-compose down`                                                 | Stop and remove running containers.       |
| `docker-compose down --volumes`                                       | Remove containers and volumes (reset DB). |
| `docker-compose -f docker-compose-deploy.yml up -d`                   | Start app in detached deployment mode.    |

---

## ☁️ Deployment

### 🟣 Deployment on **PythonAnywhere**

1. **Database:**
   Update `DATABASES` in `settings.py` to use MySQL.

2. **Collect Static Files:**

   ```bash
   python manage.py collectstatic
   ```

3. **Environment Variables:**
   Store secrets securely in `.env` or PythonAnywhere’s web settings.

4. **Deploy:**
   Upload your code and follow PythonAnywhere’s deployment instructions.

---

### 🟢 Deployment on **AWS EC2 with Docker & PostgreSQL**

You can deploy the Django Recipe API on your **EC2 instance** using Docker Compose (with PostgreSQL running as a container).

1. **SSH into your EC2 instance:**

   ```bash
   ssh -i your-key.pem ec2-user@your-ec2-public-dns
   ```

2. **Install Docker & Docker Compose:**

   ```bash
   sudo apt update
   sudo apt install docker.io docker-compose -y
   sudo systemctl enable docker
   ```

3. **Clone your repository:**

   ```bash
   git clone https://github.com/akshatraj26/Django-Recipe-API.git
   cd Django-Recipe-API
   ```

4. **Edit `.env` file:**
   Update `DJANGO_ALLOWED_HOSTS` with your EC2 public DNS (replace the below with yours):

   ```.env
   DJANGO_ALLOWED_HOSTS=your public dns from network section of ec2 instance
   ```

5. **Deploy using Docker Compose:**

   ```bash
   docker-compose -f docker-compose-deploy.yml up -d
   ```

6. **Verify containers:**

   ```bash
   docker ps
   ```

7. **Access the app:**
   Visit:

   ```
   http://<your-ec2-public-dns>:8000/api/docs/
   ```

8. **Optional Cleanup Commands:**

   ```bash
   docker-compose down
   docker-compose down --volumes
   ```

---

## 📂 Project Structure

```
Django-Recipe-API/
│
├── app/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
│
├── core/
│   ├── models.py
│   ├── admin.py
│   ├── management/
│   │   └── commands/
│   │       └── wait_for_db.py
│   └── tests/
│       ├── test_models.py
│       ├── test_commands.py
│       ├── test_admin.py
│       └── test_health_check.py
│
├── recipe/
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── tests/
│       ├── test_recipe_api.py
│       ├── test_tags_api.py
│       └── test_ingredients_api.py
│
├── user/
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── tests/
│       └── test_user_api.py
│
├── Dockerfile
├── docker-compose.yml
├── docker-compose-deploy.yml
├── requirements.txt
├── manage.py
└── README.md
```

---

## 🧭 Usage

After setup or deployment, key endpoints include:

* `/api/recipes/` – CRUD for recipes
* `/api/token/` – Token authentication
* `/api/doc/` – Swagger documentation

**Live API:** [https://akshatraj26.pythonanywhere.com/api/docs/](https://akshatraj26.pythonanywhere.com/api/docs/)

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

