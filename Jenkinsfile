pipeline {

    agent any 

    environment {
        $IMAGE_NAME = "homei"
        $CONTAINER_NAME = "homec"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning Repo ...'
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image ...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        
        stage('Remove Old Container') {
            steps {
                echo 'Removing Old Container ...'
                sh 'docker rm -f $CONTAINER_NAME || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8081:80 $IMAGE_NAME'
            }
        }

        stage('Verify Deployment') {
            steps {
                echo 'Verifying ...'
                sh 'docker ps'
            }
        }
    }
    post {
        success {
            echo 'Pipeline Running !'
        }

        failure {
            echo 'Pipeline Failed !'
        }

        always {
            echo 'Pipeline Finished !'
        }
    }
}