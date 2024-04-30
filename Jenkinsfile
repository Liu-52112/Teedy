// pipeline {
//   agent any
//     stages {
//       stage('Build') {
//         steps {
//           sh 'mvn -B -DskipTests clean package'
//         }
//     }
//   }
// }

// pipeline {
//   agent any
//     stages {
//       stage('Build') {
//         steps {
//           sh 'mvn -B -DskipTests clean package'
//           }
//         }
//         stage('pmd') {
//           steps {
//           sh 'mvn pmd:pmd'
//           }
//       }
//     }
//     post {
//       always {
//       archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
//       archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
//       archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
//     }
//   }
// }

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('PMD') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }

        stage('DOC') {
            steps {
                sh 'mvn javadoc:javadoc --fail-never '
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*-tests.jar', fingerprint: true
                }
            }
        }
    }


    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
