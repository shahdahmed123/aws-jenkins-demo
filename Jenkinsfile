pipeline {
    agent any

    triggers {
        // cron job runs every 1 hour
        cron('H * * * *')
    }

    environment {
        // استخدمي Jenkins credentials مباشرة
        AWS_CREDS = credentials('aws-creds')
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "📦 Checking out GitHub repository..."
                git branch: 'main', url: 'https://github.com/shahdahmed123/aws-jenkins-demo.git'
            }
        }

        stage('Run AWS Script') {
            steps {
                script {
                    echo "🚀 Running AWS script using Jenkins credentials..."
                    sh '''
                        chmod +x aws_script.sh
                        export AWS_ACCESS_KEY_ID=$(echo $AWS_CREDS | cut -d: -f1)
                        export AWS_SECRET_ACCESS_KEY=$(echo $AWS_CREDS | cut -d: -f2)
                        export AWS_DEFAULT_REGION=us-east-1
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
