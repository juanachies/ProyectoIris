# Proyect Iris

AI-powered platform for sign language recognition and translation using Computer Vision and Deep Learning, designed to enable more accessible communication between deaf and hearing people.

## About the Project

**Proyect Iris** is an artificial intelligence project focused on developing a platform capable of interpreting sign language through computer vision and machine learning.

The initial goal is to process video captured from a camera, extract relevant visual information such as hand, body, and facial movements, and use deep learning models to recognize and eventually translate sign language sequences into spoken-language text.

The project is designed with a long-term vision of becoming a scalable communication platform that can support different sign languages and real-world use cases.

The initial development stage will focus on:

* Computer Vision and visual feature extraction.
* Sign language recognition.
* Temporal sequence modeling.
* Sign language translation.
* A web-based interface.
* A scalable backend architecture.

The initial implementation will be developed using existing sign language datasets, with the possibility of creating and incorporating proprietary datasets in later stages.

---

## Project Architecture

At a high level, Iris follows this pipeline:

```text
Camera / Video
      ↓
Computer Vision
      ↓
Visual Representation
      ↓
Temporal Model
      ↓
Recognition / Translation
      ↓
Text Output
      ↓
Web Interface
```

The project is divided into three main technical areas:

* **Frontend:** User interface and interaction with the application.
* **Backend:** API, application logic, and communication between the frontend and ML components.
* **Machine Learning:** Data processing, experimentation, model training, evaluation, and inference.

Docker is used to provide a consistent development environment across different machines.

---

## Tech Stack

### Frontend

* React
* Vite
* JavaScript

### Backend

* Python
* FastAPI
* Docker

### Machine Learning

* Python
* PyTorch
* Computer Vision
* Deep Learning
* Jupyter Notebooks

### Development

* Git
* GitHub
* Docker
* Docker Compose

> The technology stack may evolve as the project develops.

---

## Getting Started

### Prerequisites

Make sure you have installed:

* [Docker](https://www.docker.com/)
* Git

Node.js and Python are not necessarily required on the host machine when working through Docker, depending on the current Docker configuration.

### Clone the repository

```bash
git clone <repository-url>
cd proyecto-iris
```

### Environment variables

If the project requires environment variables, copy the example file:

```bash
cp .env.example .env
```

Configure the variables according to your local environment.

**Never commit `.env` files containing secrets or private credentials.**

### Run with Docker

Build and start the application using Docker Compose:

```bash
docker compose up --build
```

Once the containers are running, the frontend and backend will be available at the ports defined in `docker-compose.yml`.

To stop the application:

```bash
docker compose down
```

### Running in the background

To start the containers in detached mode:

```bash
docker compose up --build -d
```

To view the logs:

```bash
docker compose logs -f
```

---

## Project Structure

The repository is organized into separate areas to keep the application, machine learning experiments, data, and documentation independent.

```text
proyecto-iris/
│
├── .github/
├── backend/
├── frontend/
├── ml/
├── data/
├── docs/
├── scripts/
│
├── .dockerignore
├── .env.example
├── .gitignore
├── docker-compose.yml
├── Makefile
├── README.md
└── LICENSE
```

### `.github/`

Contains GitHub-related configuration.

```text
.github/
└── workflows/
```

This folder is intended for:

* CI/CD workflows.
* Automated tests.
* Build checks.
* Future deployment automation.

Team members should not place application code here.

---

### `backend/`

Contains the backend application and API.

```text
backend/
├── app/
│   ├── api/
│   ├── core/
│   ├── schemas/
│   ├── services/
│   └── main.py
├── tests/
├── Dockerfile
└── requirements.txt
```

#### `backend/app/api/`

Contains API routes and endpoints.

Example:

```text
api/
├── routes/
│   ├── health.py
│   └── translation.py
└── dependencies.py
```

This is where HTTP endpoints should be defined.

#### `backend/app/core/`

Contains application-wide configuration and core functionality.

Examples:

* Environment configuration.
* Logging.
* Application settings.

#### `backend/app/schemas/`

Contains data schemas used by the API.

For example, request and response models using Pydantic.

#### `backend/app/services/`

Contains the application's business logic.

Examples:

* Translation services.
* Model inference services.
* Communication with external components.

API routes should remain lightweight and delegate actual logic to services whenever possible.

#### `backend/tests/`

Contains backend tests.

---

### `frontend/`

Contains the React application.

The initial structure is generated by Vite.

```text
frontend/
├── public/
├── src/
├── Dockerfile
└── package.json
```

The `src/` directory should contain all frontend application code.

As the application grows, reusable functionality can be organized into folders such as:

```text
src/
├── components/
├── pages/
├── services/
├── hooks/
├── contexts/
└── utils/
```

Do not create folders unnecessarily. Add new structures when the application actually requires them.

#### Frontend responsibilities

The frontend should handle:

* User interface.
* Camera interaction.
* User input.
* Displaying translation results.
* Communication with the backend API.

Machine learning logic should not be implemented directly inside the React application.

---

### `ml/`

Contains all machine learning development and experimentation.

```text
ml/
├── notebooks/
├── models/
│   ├── recognition/
│   └── translation/
└── README.md
```

This is where most experimentation with datasets and models will take place.

#### `ml/notebooks/`

Contains Jupyter notebooks used for:

* Dataset exploration.
* Data preprocessing.
* Feature extraction.
* Model experimentation.
* Training.
* Evaluation.
* Research.

Notebooks should use clear, descriptive names.

Example:

```text
01_exploration.ipynb
02_preprocessing.ipynb
03_baseline.ipynb
04_training.ipynb
05_evaluation.ipynb
```

When creating a new experiment, document what the notebook does and what model or approach it evaluates.

#### `ml/models/`

Contains trained models generated during development.

```text
models/
├── recognition/
└── translation/
```

Models should be separated according to their purpose.

For example:

```text
recognition/
├── baseline.pth
└── transformer_v1.pth

translation/
└── ...
```

Large model files should generally **not be committed directly to Git**. The repository should instead document where the required model can be obtained.

---

### `data/`

Contains datasets and processed data used by the project.

```text
data/
├── raw/
├── processed/
└── README.md
```

#### `data/raw/`

Contains original datasets without modifications.

#### `data/processed/`

Contains datasets generated after preprocessing or transformation.

#### Important

Datasets should generally **not be committed to Git**.

The `data/README.md` file should document:

* Dataset name.
* Source.
* How to obtain it.
* Expected directory structure.
* Preprocessing requirements.
* Relevant licenses or usage restrictions.

---

### `docs/`

Contains project documentation.

```text
docs/
├── architecture/
├── datasets/
└── research/
```

Use this folder for information that should be shared between all team members but does not belong directly in the source code.

Examples:

* Architecture diagrams.
* Dataset documentation.
* Research notes.
* Technical decisions.
* Development guidelines.

If an important architectural decision is made, document it here so that the reasoning is not lost.

---

### `scripts/`

Contains reusable scripts that support development but are not part of the main application.

Examples:

* Dataset preparation.
* Environment setup.
* Utility scripts.
* Development automation.

Scripts should not contain core backend or frontend application logic.

---

### Keep responsibilities separated

* `frontend/` → user interface.
* `backend/` → API and application logic.
* `ml/` → machine learning research and models.
* `data/` → datasets.
* `docs/` → documentation.
* `scripts/` → development utilities.

---

## Commit Conventions

To keep the project history clear and consistent, commits should follow this format:

```text
<type>(<scope>): <description>
```

### Types

* `feat` — New functionality or project feature.
* `fix` — Bug fixes or corrections.
* `docs` — Documentation changes.
* `chore` — Configuration, dependencies, infrastructure, or other maintenance tasks.

### Scopes

The scope identifies the main area affected by the commit:

* `frontend`
* `backend`
* `ml`
* `data`
* `docs`
* `infra`

### Examples

```text
feat(frontend): add camera component
feat(ml): implement baseline recognition model
fix(backend): handle invalid translation request
docs(ml): document dataset preprocessing
chore(infra): configure Docker Compose
```

The scope can be omitted when the change affects the project as a whole.

Keep commit messages concise and describe the main change introduced by the commit.

--- 

## Future Vision

The long-term goal of Proyecto Iris is to develop a scalable AI-powered communication platform capable of supporting multiple sign languages.

The initial system will focus on sign language recognition and translation into text. Future versions may explore:

* Real-time translation.
* Audio output.
* Context-aware translation.
* Mobile applications.
* API integrations.
* Institutional deployments.
* Proprietary sign language datasets.
* Support for multiple sign languages.
* Bidirectional communication.
* Sign language generation through virtual avatars.