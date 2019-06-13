pipeline {
    agent {
        docker {
            image 'docker:1.12.6'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker version'
            }
        }
    }
}
