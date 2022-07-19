@Library("jenkins-shared-library@kaiburr") _
pipeline {
    agent any
    tools {
        nodejs 'nodejs-16.10'
    }
    stages {
        stage('Checkout') {
            steps {
              deleteDir()
              echo "Checking out....."
              checkout scm
            }
        }
        stage('Build App') {
            steps {
                AppBuild()
            }
        }
        stage('Create Prod Build') {
            steps {
                NPMBuild("prod")
            }
        }
        stage('Docker Build') {
            steps {
                DockerBuild()
            }
        }
    }
}
