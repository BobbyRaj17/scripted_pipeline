pipeline {
    agent {
        docker {
            image 'docker:1.12.6'
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
