pipeline {
    agent any

    stages {
        stage('Check Tofu version') {
            steps {
                sh 'tofu -v'
            }
        }
        stage('Check out configuration repo') {
            steps{
                git branch: 'main', credentialsId: 'S8-JenkinsID', url: 'ssh://git@bitbucket.local:23/s8/cpp-template.git'
            }
        }
        stage('Start Tofu') {
            steps {
                dir('terraform') {
                    sh 'tofu destroy -auto-approve'
                    sh 'tofu init'
                    sh 'tofu apply -auto-approve'
                }
            }
        }
    }
    post {
      always {
            cleanWs()
          dir('terraform') {
              sh 'tofu destroy -auto-approve'
          }
      }
    }
}

