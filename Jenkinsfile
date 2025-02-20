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
                git branch: 'master', credentialsId: 'S8-JenkinsID', url: 'ssh://git@bitbucket.local:23/s8/cpp-template.git'
            }
        }
        stage('Start Tofu') {
            steps {
                sh 'ls -la'
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
            archiveArtifacts artifacts: '**/*.exe', followSymlinks: false
            dir('terraform') {
                sh 'tofu destroy -auto-approve'
            }
            cleanWs()
      }
    }
}

