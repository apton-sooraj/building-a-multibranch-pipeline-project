pipeline {
  environment {
    registry = "aptonsooraj/test-pipeline"
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
    stage('Develop Branch Deploy Code') {
      when {
        branch 'development'
      }
      steps {
        script {
          docker.build registry + ":$BUILD_NUMBER"
        }

      }

    }

    stage('Deploy Image') {
              when {
        branch 'development'
      }
      steps {
        script {
          docker.withRegistry('', registryCredential) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
              when {
        branch 'development'
      }
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }

    stage('production Branch Deploy Code') {
              when {
        branch 'development'
      }
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