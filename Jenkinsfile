pipeline {
agent any

```
environment {
    DOCKER_IMAGE = "https://hub.docker.com/repository/docker/rawdaessamrou/flask-app"
    DOCKER_TAG = "${BUILD_NUMBER}"
    CONTAINER_NAME = "flask-container"
}

stages {

    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Build Docker Image') {
        steps {
            script {
                docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
            }
        }
    }

    stage('Login to DockerHub') {
        steps {
            withCredentials([usernamePassword(
                credentialsId: 'dockerhub-credentials',
                usernameVariable: 'DOCKER_USER',
                passwordVariable: 'DOCKER_PASS'
            )]) {
                sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
            }
        }
    }

    stage('Push Image') {
        steps {
            script {
                docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").push()
            }
        }
    }

    stage('Deploy Container') {
        steps {
            script {
                sh """
                docker stop ${CONTAINER_NAME} || true
                docker rm ${CONTAINER_NAME} || true
                docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${DOCKER_IMAGE}:${DOCKER_TAG}
                """
            }
        }
    }
}

post {
    always {
        sh "docker logout"
    }
}
```

}
