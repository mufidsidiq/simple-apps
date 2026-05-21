pipeline {
    agent {label 'DevOps1'}
    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/mufidsidiq/simple-apps.git'
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
                sonar \
                 -Dsonar.host.url=http://172.23.7.211:9000 \
                 -Dsonar.token=sqp_4f9c1d84c7814b12db85541064347fb403764960 \
                 -Dsonar.projectKey=simple-apps'''
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