pipeline{
    agent any

    environment {
        IMAGE_NAME = "thealamdev/my-app"
        IMAGE_TAG = "latest"
        PATH = "/usr/local/bin:/opt/homebrew/bin:${env.PATH}"
    }

    stages {
        stage("build"){
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage("run"){
            steps {
                script {
                    sh "docker run -d -p 5001:5000 --name demo-container ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}