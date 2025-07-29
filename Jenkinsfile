pipeline {
    agent any

    environment {
        VENV_DIR = 'venv'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/IMugisha-io/june25-classdemo2.git'
            }
        }

        stage('Set up Python Environment') {
            steps {
                bat '''
                    python -m venv %VENV_DIR%
                    call %VENV_DIR%\\Scripts\\activate.bat
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Apply Migrations') {
            steps {
                bat '''
                    call %VENV_DIR%\\Scripts\\activate.bat
                    python manage.py migrate
                '''
            }
        }

        stage('Run Tests (Optional)') {
            steps {
                bat '''
                    call %VENV_DIR%\\Scripts\\activate.bat
                    python manage.py test
                '''
            }
        }

        stage('Run Server') {
            steps {
                bat '''
                    call %VENV_DIR%\\Scripts\\activate.bat
                    start /b python manage.py runserver 0.0.0.0:8000
                '''
            }
        }
    }

    post {
        success {
            echo 'Django server deployed successfully! bingo'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
