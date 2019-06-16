// pipeline {
//     agent none
//     stages {
//         stage('Build') {
//             agent {
//               image 'docker:1.12.6'
//               args '-v /var/run/docker.sock:/var/run/docker.sock'
//             }
//             steps {
//                 sh 'docker version'
//                 sh 'docker build -t test .'
//             }
//         }
//         stage('Helm') {
//             agent {
//                 docker { image 'alpine/helm:2.14.0' }
//                 args '-v ${workspace}:/apps'
//                 args '-v ~/.kube/config:/root/.kube/config'
//             }
//             steps {
//                 sh 'which helm'
//                 sh 'helm init'
//             }
//         }
//     }
// }
pipeline {
    agent none
    environment {
      PATH = "/usr/local/bin/docker:$PATH"
    }
    stages {
      stage('source') {
          agent any
          steps {
              sh 'source /etc/profile'
            }
        }
        stage('Back-end') {
            agent {
                docker {
                  image 'maven:3-alpine'
                  args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                sh 'mvn --version'
            }
        }
        stage('Front-end') {
            agent {
                docker { image 'lachlanevenson/k8s-helm:v2.6.0' }
            }
            steps {
                sh 'which helm'
                sh 'ls'
            }
        }
    }
}
