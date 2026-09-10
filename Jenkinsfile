pipeline {

    agent any

    environment {
        IMAGE_NAME = "vaishnavi3008/hello-world"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Git Pull') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/vaishnavi1965/hello-world-devops.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=hello-world-devops \
                        -Dsonar.projectName=hello-world-devops \
                        -Dsonar.sources=app
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t $IMAGE_NAME:$IMAGE_TAG .
                '''
            }
        }

        stage('Push Image to Registry') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push $IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    sed -i "s|image: .*|image: $IMAGE_NAME:$IMAGE_TAG|" k8s/deployment.yaml
                    kubectl apply -f k8s/deployment.yaml
                    kubectl apply -f k8s/service.yaml
                '''
            }
        }
    }
}