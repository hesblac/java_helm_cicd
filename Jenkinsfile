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
                            docker build -t 44.210.129.66:8083/springapp:${VERSION} .

                            docker login -u admin -p hesblac 44.210.129.66:8083

                            docker push 44.210.129.66:8083/springapp:${VERSION}

                            docker rmi 44.210.129.66:8083/springapp:${VERSION}   
                        """
                    }
                    

                }
            }
        }
        stage('identifying misconfigs using datree in helmchart'){

            steps{

                script{
                    dir('kubernetes/myapp/templates/') {
                        withEnv(['DATREE_TOKEN=da46896b-9718-4dc0-8f65-3e516a1cbf91']) {
                        
                            sh 'helm datree test deployment.yaml' 
                        }
                   
                    }

                }
            }
        }
        stage('pushing the helm chat to nexus repo.'){

            steps{

                script{
                withCredentials([string(credentialsId: 'nexus_passwd', variable: 'nexus_creds')]) {
                     dir('kubernetes/myapp/') {
                    sh '''
                    helmversion=$(helm show chart myapp | grep version | cut -d -f 2 | tr -d ' ')
                    tar -tzf myapp-${helmversion}.tgz myapp/
                    curl -u admin:$nexus_password http://44.210.129.66:8081/repository/helm-repo/ --upload-file myapp-${helmversion}.tgz -v '
                    '''
                    }
                }
                }
            }
        }
    }
    post {
		always {
			mail bcc: '', body: "<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "${currentBuild.result} CI: Project name -> ${env.JOB_NAME}", to: "hesblac.demo@gmail.com";  
		}
	}
}

