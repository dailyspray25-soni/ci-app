pipeline {
    agent any

    stages {
        stage('Build JAR') {
            steps {
                sh 'mvn clean package'
            }
        }

     stage('Build Docker Image') {
            steps {
                sh 'docker build -t ci-app-image .'
            }
        }

     stage('Deploy Container') {
       steps {
         sh 'docker stop ci-app || true'
         sh 'docker rm ci-app || true'
         sh 'docker run -d --name ci-app ci-app-image'
       }
      }
     }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
