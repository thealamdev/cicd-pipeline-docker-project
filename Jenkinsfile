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
                    echo "=== build the image lastest version ==="
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

    post {
        success {
            emailext subject: "Build SUCCESS: ${JOB_NAME}",
                     body: "Job ${JOB_NAME} build #${BUILD_NUMBER} was successfull",
                     to: "pakhiba407@gmail.com"

            slackSend(
                channel: '#jenkins-deploy-updates',
                message: "SUCCESS: ${JOB_NAME} #${BUILD_NUMBER} completed successfully.",
                color: 'good'
            )
        }

        failure {
            emailext subject: 'Build FAILURE: ${JOB_NAME}',
                     body: "Job ${JOB_NAME} build #${BUILD_NUMBER} failed.",
                     to: "pakhiba407@gmail.com"

            slackSend(
                channel: '#jenkins-deploy-updates',
                message: "FAILURE: ${JOB_NAME} #${BUILD_NUMBER} failed. Please check the Jenkins console output.",
                color: 'danger'
            )
        }
    }
}