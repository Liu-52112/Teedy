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

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    surefire '**/target/surefire-reports/*.xml'
                    javadoc javadocDir: 'target/site/apidocs', keepAll: false
                }
            }
        }

        stage('PMD') {
            steps {
                sh 'mvn pmd:pmd'
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/site/pmd.html'
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
