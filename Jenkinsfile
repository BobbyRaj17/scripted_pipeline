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
                sh 'pwd'
                sh 'hostname'
                sh 'ls -ltr'
                sh 'docker build -t test .'
            }
        }
    }
}
