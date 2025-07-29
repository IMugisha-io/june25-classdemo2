
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
                sh '''
                    python3 -m venv $VENV_DIR
                    source $VENV_DIR/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Apply Migrations') {
            steps {
                sh '''
                    source $VENV_DIR/bin/activate
                    python manage.py migrate
                '''
            }
        }

        stage('Run Tests (Optional)') {
            steps {
                sh '''
                    source $VENV_DIR/bin/activate
                    python manage.py test || true
                '''
            }
        }

        stage('Run Server') {
            steps {
                sh '''
                    source $VENV_DIR/bin/activate
                    nohup python manage.py runserver 0.0.0.0:8000 &
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
