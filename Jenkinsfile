@Library('container-lib@main') _
// Alternatively, if you want to load the library dynamically from GitHub without global config:
// @Library(identifier: 'k8s-deploy-library@main', changelog: false) _
pipeline {
    agent any
    environment {
        APP_NAME      = 'myapp'
        IMAGE_TAG     = "${env.BUILD_NUMBER}"       // Use Jenkins build number as tag
        REGISTRY      = 'ghcr.io/your-org'          // Example: GitHub Container Registry
        DOCKER_IMAGE  = "${REGISTRY}/${APP_NAME}:${IMAGE_TAG}"
    }
    stages {
        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                script {
                    buildAndPushContainerImage(
                        image: "${DOCKER_IMAGE}"
                    )
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    deployToK8s(
                        deploymentName: "${APP_NAME}",
                        image: "${DOCKER_IMAGE}"
                    )
                }
            }
        }
    }
    post {
        success {
            echo "Successfully deployed ${DOCKER_IMAGE} to Kubernetes"
        }
        failure {
            echo "Build or deployment failed"
        }
    }
}