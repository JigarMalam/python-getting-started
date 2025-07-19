pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    echo "Deploying app..."
                    # Add deployment steps here
                '''
            }
        }
    }

    post {
        success {
            echo "Sending Email"
            mail to: 'jigarmalam13@gmail.com',
                 subject: "SUCCESS: Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                 body: "Job succeeded: ${env.BUILD_URL}"
        }

        failure {
            echo "Sending Email"
            mail to: 'jigarmalam13@gmail.com',
                 subject: "FAILURE: Jenkins Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                 body: "Job failed: ${env.BUILD_URL}"
        }
    }
}
