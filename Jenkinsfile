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
                sh 'mvn test'  // Add test to your pipeline
            }
            post {
                always {
                    surefire '**/target/surefire-reports/*.xml'  // Generate sure-fire report as artifact
                    javadoc javadocJar: true  // Generate javadoc (mvn javadoc:jar) as artifact
                }
            }
        }

        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
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
