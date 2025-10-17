pipeline {
    agent any

    triggers {
        // cron job runs every 1 hour
        cron('H * * * *')
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
                echo "🚀 Running AWS script using Jenkins AWS credentials..."
                withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                    sh '''
                        echo "🔐 AWS credentials loaded successfully"
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
