pipeline {
  environment {
    imagename = "aptonsooraj/test-pipeline"
    registryCredential = 'dockerhub'
  }
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
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }

    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BRANCH_NAME+$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

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