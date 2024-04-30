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
                sh 'mvn test' // 运行测试用例
            }
            post {
                always {
                    surefire '**/target/surefire-reports/*.xml' // 生成测试报告
                    javadoc javadocDir: 'target/site/apidocs' // 生成 Javadoc
                }
            }
        }

        stage('PMD') {
            steps {
                sh 'mvn pmd:pmd' // 运行 PMD 代码分析
            }
            post {
                always {
                    archiveArtifacts artifacts: '**/target/site/pmd.html' // 归档 PMD 报告
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true // 归档所有站点文件
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true // 归档 JAR 文件
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true // 归档 WAR 文件
        }
    }
}
