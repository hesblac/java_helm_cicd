// pipeline {

//     agent any

//     stages {

//         stage('Sonar quality check') {
            
//             agent{

//                 docker{
//                     image 'maven'
//                 }
//             }
//             steps{

//                 script{

//                     withSonarQubeEnv(credentialsId: 'sonar-pass') {
//                         sh 'mvn clean package sonar:sonar'
//                 }
//                 }
//             }
//         }
//     }

// }



pipeline {
    agent any

    stages {
        stage('Sonar quality check') {
            agent {
                docker {
                    image 'maven:3-jdk-8'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-pass') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }
}
