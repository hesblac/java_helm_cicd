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
            
            agent any
            
            steps{

                script{

                    // Install Maven on the server
                    sh 'sudo apt update'
                    sh 'sudo apt install -y maven'

                    withSonarQubeEnv(credentialsId: 'sonar-pass') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }

}
