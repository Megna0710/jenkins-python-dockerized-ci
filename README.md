\# Jenkins Python Dockerized CI



An intermediate-level CI assignment demonstrating a Docker-based Jenkins Declarative Pipeline for Python linting, automated testing, test reporting, and coverage generation.



\## Pipeline Stages



1\. \*\*Checkout Code\*\* — retrieves the source from the configured repository.

2\. \*\*Set Up Environment\*\* — creates a Python virtual environment and installs dependencies.

3\. \*\*Lint\*\* — runs Flake8 against the application and test files.

4\. \*\*Run Tests\*\* — executes pytest and generates JUnit XML and coverage reports.

5\. \*\*Archive Reports\*\* — publishes the JUnit results and archives the coverage report.



The Jenkins agent uses `python:3.11-slim`. The separate Flask application uses the Ubuntu-based Dockerfile.



\## Components



\- `app.py` — arithmetic functions.

\- `tests/test\_app.py` — unit tests.

\- `requirements.txt` — Python dependencies.

\- `Jenkinsfile` — Jenkins Declarative Pipeline.

\- `app1.py` — Flask web application.

\- `Dockerfile` — container definition for the Flask application.

\- `.github/workflows/python-variables.yml` — GitHub Actions variable-scope demonstration.



\## Local Verification



Install dependencies:



```bash

python -m pip install -r requirements.txt

```



Run tests:



```bash

python -m pytest tests/ -v

```



Run linting:



```bash

python -m flake8 app.py app1.py tests/

```



\## Jenkins Reports



\- JUnit test report: `reports/test-results.xml`

\- Coverage report: `coverage.xml`



Jenkins publishes the JUnit results and archives the coverage XML file. The workspace is cleaned after each build.



\## GitHub Actions



The workflow demonstrates workflow-level, job-level, and step-level environment variables. It can be triggered by a push to `main` or manually through GitHub Actions.



\## Repository



This project demonstrates Python CI automation using Jenkins, Docker, Flake8, pytest, and coverage reporting.



