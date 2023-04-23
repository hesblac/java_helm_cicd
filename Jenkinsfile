pipeline {

    agent any

    stages {
        stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'Default Maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=sonarjenks -Dsonar.projectName='sonarjenks'"
    }
  }

    //     stage('Sonar quality check') {
            
    //         agent{

    //             docker{
    //                 image 'maven'
    //                // args '-u root --userns=host'
    //             }
    //         }
    //         steps{

    //             script{

    //                 withSonarQubeEnv(credentialsId: 'sonar-jenk') {
    //                     sh 'mvn clean package sonar:sonar'
    //             }
    //             }
    //         }
    //     }
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
