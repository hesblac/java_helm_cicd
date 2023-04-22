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

                    withSonarQubeEnv(credentialsId: 'sonar-pass') {
                        sh 'mvn clean package sonar:sonar'
                }
                }
            }
        }
    }

}



