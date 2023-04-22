pipeline {

    agent any
    environment {
        SONAR_LOGIN = credentials('sonarqube-login')
        MAVEN_OPTS = '-Dmaven.repo.local=/home/jenkins/.m2/repository'
    }
    stages {

        stage('sonear quality check') {
            
            agent{

                docker{
                    image 'maven'
                }
            }
            steps{

                script{

                    withSonarQubeEnv(credentialsId: 'sonar-tokin') {
                        sh 'mvn clean package sonar:sonar'
                }
                }
            }
        }
    }

}