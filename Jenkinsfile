```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                    python -m venv .venv
                    .venv\\Scripts\\python.exe -m pip install --upgrade pip
                    .venv\\Scripts\\python.exe -m pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                bat '.venv\\Scripts\\python.exe -m pytest -v'
            }
        }

        stage('Run Application') {
            steps {
                bat '.venv\\Scripts\\python.exe app.py'
            }
        }

        stage('Package Release') {
            steps {
                bat '''
                    if not exist release mkdir release
                    copy app.py release\\app.py
                    copy requirements.txt release\\requirements.txt
                '''
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Student Management CI/CD Pipeline completed!'
        }
        failure {
            echo 'FAILED: Check Console Output.'
        }
    }
}
```
