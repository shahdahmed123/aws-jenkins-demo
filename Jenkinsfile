pipeline {
    agent any

    triggers {
        cron('H * * * *') // runs every 1 hour
    }

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/USERNAME/REPO.git'
            }
        }

        stage('Run AWS Action') {
            steps {
                withAWS(credentials: 'aws-creds') {
                    sh '''
                        chmod +x run_aws_action.sh
                        ./run_aws_action.sh
                    '''
                }
            }
        }
    }
}
