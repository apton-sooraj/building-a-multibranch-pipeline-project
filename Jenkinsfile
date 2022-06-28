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
