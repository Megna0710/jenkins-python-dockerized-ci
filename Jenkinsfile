
pipeline {
    agent {
        docker {
            image 'python:3.11-slim'
            args '-u root'
        }
    }

    environment {
        PYTHONPATH = '.'
    }

    options {
        timeout(time: 10, unit: 'MINUTES')
        timestamps()
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Set Up Environment') {
            steps {
                sh '''
                    python --version
                    python -m venv .venv
                    . .venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Lint') {
            steps {
                sh '''
                    . .venv/bin/activate
                    flake8 app.py app1.py tests/
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . .venv/bin/activate
                    mkdir -p reports
                    pytest tests/ \
                        --junitxml=reports/test-results.xml \
                        --cov=app \
                        --cov-report=xml:coverage.xml
                '''
            }
        }

        stage('Archive Reports') {
            steps {
                junit 'reports/test-results.xml'

                archiveArtifacts(
                    artifacts: 'coverage.xml',
                    allowEmptyArchive: true
                )
            }
        }
    }

    post {
        always {
            cleanWs()
        }

        success {
            echo 'Build Passed'
        }

        failure {
            echo 'Build Failed'
        }
    }
}
