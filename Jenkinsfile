pipeline {

    agent any

    stages {

        stage('Sonar quality check') {
            
            agent{

                docker{
                    image 'maven'
                }
            }
            steps{

                script{

                    withSonarQubeEnv(credentialsId: 'sonar-jenk') {
                        sh 'mvn clean package sonar:sonar'
                }
                }
            }
        }
    }

}


// pipeline {

//     agent any

//     stages {

//         stage('Sonar quality check') {
            
//             // agent any
            
//             steps{

//                 script{

//                     // // Install Maven on the server
//                     // sh 'sudo -S apt update'
//                     // sh 'sudo -S apt install -y maven'

//                     withSonarQubeEnv(credentialsId: 'sonar-jenk') {
//                         sh 'mvn clean package sonar:sonar'
//                     }
//                 }
//             }
//         }
//     }

// }
