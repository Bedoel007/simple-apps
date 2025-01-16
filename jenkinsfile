pipeline {
 agent {
  label 'devops1-kiki'
}

    tools {
  nodejs 'nodejs'
}


    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Bedoel007/simple-apps.git'
            }
        }
        stage('Build') {
            steps {
                sh '''cd apps
                npm install'''
            }
        }
        stage('Testing') {
            steps {
                sh '''cd apps
                npm test
                npm run test:coverage'''
            }
        }
        stage('Code Review') {
            steps {
                sh '''cd apps
                 sonar-scanner \\
                 -Dsonar.projectKey=Simple-Apps   
                 -Dsonar.sources=.   
                 -Dsonar.host.url=http://172.23.10.12:9000   
                 -Dsonar.login=sqp_07ae92a9d723ee728551e76439d53de59a9edf84
                 '''
            }
        }
        stage('Deploy compose') {
            steps {
                sh '''
                docker compose build
                docker compose up -d
                '''
            }
        }
    }
}