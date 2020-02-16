pipeline {
    agent {
        docker { image 'node:7-alpine' }
    }
    stages {
        stage('Test') {
            steps {
                which docker
                sh 'node --version'
            }
        }
    }
}
