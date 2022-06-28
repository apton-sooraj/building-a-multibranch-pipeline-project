pipeline {
  environment {
    imagename = "/aptonone-qa/pipeline-test/new"
    asia-south1-docker.pkg.dev/aptonone-qa/pipeline-test
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
          docker.withRegistry( 'https://asia-south1-docker.pkg.dev', 'gcr:[test]') {
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

    stage('production Branch Deploy Codes') {

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
}