pipeline {
    agent any

    environment {
        APP_ENV = 'staging'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/JigarMalam/python-getting-started.git'
            }
        }

        stage('Build') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'pytest'
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying to staging environment...'
                // Dummy deploy command
                sh 'echo "Deployed to $APP_ENV!"'
            }
        }
    }

    post {
        success {
            mail to: 'jigarmalam13@gmail.com',
                 subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build was successful.\n\nJob: ${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}\nCheck console output: ${env.BUILD_URL}"
        }
        failure {
            mail to: 'jigarmalam13@gmail.com',
                 subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Build failed. Check console output: ${env.BUILD_URL}"
        }
    }
}
