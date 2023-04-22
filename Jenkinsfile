pipeline {

    agent any

    stages {

        stage('sonear quality check') {
            environment {
                DOCKER_IMAGE = 'maven:3-jdk-8-alpine'}
                        steps {
                        // Checkout code from version control
                        checkout([$class: 'GitSCM', branches: [[name: '*/master']], userRemoteConfigs: [[url: 'https://github.com/your/repo.git']]])

                        // Build and test the Maven project inside a Docker container
                        sh "docker run --rm -v $PWD:/app -w /app $DOCKER_IMAGE mvn clean install"

                        // Analyze the project using SonarQube
                        withSonarQubeEnv('SonarQube') {
                        sh 'mvn sonar:sonar'
                        }
                    }   
           
        }
    }

}

//  agent{

//                 docker{
//                     image 'maven'
//                 }
//             }
//             steps{

//                 script{

//                     withSonarQubeEnv(credentialsId: 'sonar-tokin') {
//                         sh 'mvn clean package sonar:sonar'
//                 }
//                 }
//             }