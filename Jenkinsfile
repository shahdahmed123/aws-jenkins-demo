pipeline {
    agent any

    triggers {
        // cron job runs every 1 hour
        cron('H * * * *')
    }

    environment {
        // Use Jenkins AWS credentials (ID = aws-creds)
        AWS_CREDS = credentials('aws-creds')
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Get the repo from GitHub
                git branch: 'main', url: 'https://github.com/shahdahmed123/aws-jenkins-demo.git'
            }
        }

        stage('Run AWS Script') {
            steps {
                withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                    sh '''
                        echo "Running AWS script using Jenkins credentials..."
                        chmod +x aws_script.sh
                        ./aws_script.sh
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ AWS job completed successfully!'
        }
        failure {
            echo '❌ AWS job failed!'
        }
    }
}
