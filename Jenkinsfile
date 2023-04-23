pipeline {

    agent any

    stages {

        stage('Sonar quality check') {
            
            agent{

                docker{
                    image 'maven'
                   // args '-u root --userns=host'
                }
            }
            steps{

                script{

                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'mvn clean package sonar:sonar'
                }
                }
            }
        }
        stage('Quality Gate status'){

            steps{

                script{
                
                waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                
                }
            }
        }
        // stage('docker build & docker push to nexus repo'){

        //     steps{

        //         script{
             

        //         }
        //     }
        // }
    }

}

