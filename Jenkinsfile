pipeline {
agent any

```
stages {
    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Install Dependencies') {
        steps {
            bat 'if not exist .venv\\Scripts\\python.exe python -m venv .venv'
            bat '.venv\\Scripts\\python.exe -m pip install --disable-pip-version-check --retries 5 --timeout 120 -r requirements.txt'
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
            bat 'if not exist release mkdir release'
            bat 'copy /Y app.py release\\app.py'
            bat 'copy /Y requirements.txt release\\requirements.txt'
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
```

}
