pipeline {
  environment {
    imagename = "aptonsooraj/test-pipeline"
    registryCredential = 'dockerhub'
  }
  agent any
  stages {
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
            dockerImage.push(env.BRANCH_NAME+"-"+ env.BUILD_NUMBER)

          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BRANCH_NAME-$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    }

    stage('production Branch Deploy Code') {

      when {
        branch 'production'
      }
      steps {
        sh """
        
        echo "Building Artifact from production brancha"
        """
        
        sh """
        
        echo "Deploying Code from production branch"
        """
        
      }
    }
  }