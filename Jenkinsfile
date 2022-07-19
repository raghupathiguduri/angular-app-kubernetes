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
        stage('Docker Build') {
          when {
              expression { params.BRANCH == 'develop' }
            }
          steps {
            withCredentials([usernamePassword(credentialsId: 'nexus', usernameVariable: 'username', passwordVariable: 'password')]) {
                DockerBuild(BUILD_NUMBER, username, password)
            }
          }
        }
    }
}
