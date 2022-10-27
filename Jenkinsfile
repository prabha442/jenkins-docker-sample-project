pipeline {
  agent any

  stages {
    stage ('git checkout'){
      steps{
          git 'https://github.com/prabha442/jenkins-docker-sample-project.git'
        }
       }
   
    stage ('docker image build'){
       steps{
         sh ' docker image build -t $JOB_NAME:v1.$BUILD_ID .'
	 sh ' docker image tag $JOB_NAME:v1.$BUILD_ID prabha442/$JOB_NAME:v1.$BUILD_ID '
	 sh ' docker image tag $JOB_NAME:v1.$BUILD_ID prabha442/$JOB_NAME:latest '

	 }
	}
	  
    stage ('docker image push to dockerhub'){
       steps{
	withCredentials([string(credentialsId: 'dockerhub-passwd', variable: 'dockerpasswd')]) {
		sh "docker login -u prabha442 -p ${dockerpasswd}"
		sh ' docker image push prabha442/$JOB_NAME:v1.$BUILD_ID '
		sh ' docker image push prabha442/$JOB_NAME:latest '
		
		sh ' docker image rm $JOB_NAME:v1.$BUILD_ID prabha442/$JOB_NAME:v1.$BUILD_ID prabha442/$JOB_NAME:latest '
               }
            }
         }
    

      }
     } 
