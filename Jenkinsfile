pipeline {
    
    agent any
    environment {

        VERSION = "${env.BUILD_ID}"
    }

    stages {

        stage('Sonar quality check') {
            
            agent{

                docker{
                    image 'maven'
                    args '-u root --userns=host'
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
                
                    waitForQualityGate abortPipeline: true, credentialsId: 'sonar-token'
                
                }
            }
        }
        stage('docker build & docker push to nexus repo'){

            steps{

                script{
                    withCredentials([string(credentialsId: 'nexus_passwd', variable: 'nexus_creds')]) {
                        sh """
                            docker build -t 44.210.129.66:8083/springapp:$[VERSION] .

                            docker login -u admin -p hesblac 44.210.129.66:8083

                            docker push 44.210.129.66:8083/springapp:$[VERSION]

                            docker rmi 44.210.129.66:8083/springapp:$[VERSION]
                            
                        """
                    }
                    

                }
            }
        }
    }

}

