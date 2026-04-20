pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    credentialsId: 'djangokey',
                    url: 'https://github.com/sunandgmohan/django-travel-app.git'
            }
        }
 
        stage('Deploy to EC2') {
            steps {
                sshagent(['django_aws']) {
                    sh '''
                        ssh -A -o StrictHostKeyChecking=no ubuntu@52.205.98.7 \
                            "set -e && \
                            rm -rf /home/ubuntu/Djangodemo && \
                            cd /home/ubuntu/Djangodemo
                            git clone git@github.com:sunandgmohan/django-travel-app.git && \
                            cd /home/ubuntu/Djangodemo/django-travel-app.git && \
                            docker build -t myapp . && \
                          
                            docker build -d -p 7000:8000 myapp"
                    '''
                }
            }
        }
    }
}

