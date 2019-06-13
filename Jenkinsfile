// pipeline {
//     agent {
//         docker {
//             image 'docker:1.12.6'
//             args '-v /var/run/docker.sock:/var/run/docker.sock'
//         }
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'docker version'
//                 sh 'pwd'
//                 sh 'hostname'
//                 sh 'ls -ltr'
//                 sh 'docker build -t test .'
//             }
//         }
//     stage('Helm') {
//       agent {
//         docker {
//           image 'lachlanevenson/k8s-helm:v2.6.0'
//               }
//           }
//       steps {
//         sh 'which helm'
//           }
//        }
//     }
// }
pipeline {
    agent none
    stages {
        stage('Back-end') {
            agent {
                docker { image 'maven:3-alpine' }
            }
            steps {
                sh 'mvn --version'
            }
        }
        stage('Front-end') {
            agent {
                docker { image 'node:7-alpine' }
            }
            steps {
                sh 'node --version'
            }
        }
    }
}
