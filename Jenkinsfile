pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/kruthikav04/Simple.git'
            }
        }

        stage('Create Virtual Env') {
            steps {
                sh '''
                    python3 -m venv venv
                    chmod +x venv/bin/activate
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    ./venv/bin/pip install --upgrade pip
                    ./venv/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                    pkill -f "python app.py" || true
                    nohup ./venv/bin/python app.py > app.log 2>&1 &
                '''
            }
        }
    }
}
