pipeline {

    agent any

    environment {

        MAVEN_OPTS = '-Dmaven.repo.local=/home/jenkins/.m2/repository'
    }
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