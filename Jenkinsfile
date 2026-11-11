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
                    echo "=== build the image ==="
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }

        stage("run"){
            steps {
                script {
                    echo "=== run the image on 5001 port. You can visit : http://localhost:5001 to see the live site ==="
                    sh "docker run -d -p 5001:5000 --name demo-container ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}