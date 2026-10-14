pipeline {
    agent any

    options {
        timeout(time: 10, unit: 'MINUTES')
    }

    stages {
        stage('Setup') {
            steps {
                sh 'python3 -m venv .venv'
                sh '.venv/bin/pip install -r requirements.txt'
            }
        }
        stage('Lint') {
            steps {
                sh '.venv/bin/flake8 app.py test_app.py'
            }
        }
        stage('Test') {
            steps {
                sh '.venv/bin/pytest --junitxml=report.xml'
            }
        }
    }

    post {
        always {
            junit 'report.xml'
        }
    }
}