pipeline{
    agent any

    environment{
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "zillionclouds@gmail.com"
        POST = "3000"
    }

    stages {
        stage("Clone Repo"){
            steps{
                git branch: "main", url: "https://github.com/ZillionClouds/nestjs-jenkins-learning.git"
            }
        }

        stage("Build Docker Image"){
            steps {
                sh 'docker build -t $IMAGE_NAME'
            }
        }

        stage("Stop and Remove PRevious Container"){
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage("Run New Docker Container"){
            steps {
                sh '''
                    docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage("Send Email Notification"){
            steps {
                emailtext(
                    subject: "NestJS App Deployed Successfully!"
                    body: "Your NestJS App is deployed and Ready to use. http://13.235.13.130:${PORT}/"
                    to: "${EMAIL}"
                )
            }
        }
    }
}