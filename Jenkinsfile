// pipeline {
//     agent any
    
//     stages {
//         stage('Build') {
//             steps {
//                 bat 'mvn -B -DskipTests clean package'
//             }
//         }
// //         stage('Sonar-Report') {
// //             steps {
// //             sh 'mvn sonar:sonar \
// //   -Dsonar.projectKey=jenkins_project \
// //   -Dsonar.host.url=http://localhost:9000 \
// //   -Dsonar.login=5f09ded7e5db4d0ea0dcfd937c181af706e60475'
// //             }
// //         }
//         stage('Test') { 
//             steps {
//                 bat 'mvn test' 
//             }
//             post {
//                 always {
//                     junit 'target/surefire-reports/*.xml' 
//                 }
//             }
//         }
//         stage('Sonar-Report') {
//             steps {
//                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
//             bat """
//             mvn clean install sonar:sonar ^
//             -Dsonar.host.url=http://localhost:9000 ^
//             -Dsonar.login=%SONAR_TOKEN%
//             """
//             }
//         }
//     }
// }

//deployment
pipeline {
    agent { label 'Slave-01' }

    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Deploy') {
            agent { label 'deployment' }
            steps {
                bat 'C:\\deployment\\deployment.bat'
            }
        }
    }
}
