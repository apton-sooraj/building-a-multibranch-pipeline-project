pipeline {
    agent any
    stages {
        stage('Master Branch Deploy Code') {
            when {
                branch 'master'
            }
            steps {
                sh """
                echo "Building Artifact from Master branch"
                """
 
                sh """
                echo "Deploying Code from Master branch"
                """
            }
        }
        stage('Develop Branch Deploy Code') {
            when {
                branch 'development'
            }
            steps {
                sh """
                echo "Building Artifact from Develop branch"
                """
                sh """
                echo "Deploying Code from Develop branch"
                """
                sh 'docker build -t aptonsooraj/test-pipeline:latest .'
           }
        }
        stage('Docker Push') {
            when {
                branch 'development'
            }     
             steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker aptonsooraj/test-pipeline:latest'
        }
      }
        }

        stage('production Branch Deploy Code') {
            when {
                branch 'production'
            }
            steps {
                sh """
                echo "Building Artifact from production branch"
                """
                sh """
                echo "Deploying Code from production branch"
                """
           }
        }
    }
}
