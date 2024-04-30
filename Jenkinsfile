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
                sh 'mvn javadoc:jar || True'
            }
            post {
                success {
                    // 存储 javadoc jar 作为构建工件
                    archiveArtifacts artifacts: '**/target/*-javadoc.jar', fingerprint: true
                }
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
