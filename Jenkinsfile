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
                    # Ensure pip is installed in the venv
                    ./venv/bin/python -m ensurepip --upgrade
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    # Use python -m pip to avoid missing pip issue
                    ./venv/bin/python -m pip install --upgrade pip
                    ./venv/bin/python -m pip install -r requirements.txt
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                    # Stop any old running instance of the app
                    pkill -f "python app.py" || true

                    # Run Flask app in background
                    nohup ./venv/bin/python app.py > app.log 2>&1 &
                '''
            }
        }
    }
}
