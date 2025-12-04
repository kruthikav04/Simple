pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/kruthikav04/Simple.git'
            }
        }

        stage('Deploy to VM') {
            steps {
                sshagent(['vm-ssh']) {
                    sh '''
                    scp -o StrictHostKeyChecking=no -r * backup_gcp@10.4.4.70:/home/backup_gcp/simple

                    ssh -o StrictHostKeyChecking=no backup_gcp@10.4.4.70 "
                        cd /home/backup_gcp/simple
                        pkill -f 'python3 app.py' || true
                        python3 -m venv venv
                        ./venv/bin/pip install -r requirements.txt
                        nohup ./venv/bin/python app.py > app.log 2>&1 &
                    "
                    '''
                }
            }
        }
    }
}

