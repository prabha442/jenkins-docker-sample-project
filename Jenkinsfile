pipeline {
  agent any

  stages {
    stage ('git checkout'){
      steps{
       sh "git 'https://github.com/prabha442/jenkins-docker-sample-project.git'"
        }
       }
   
    stage ('docker image build'){
       steps{
         sh ' docker image build -t $JOB_NAME:v1.$BUILD_ID .'
	 sh ' docker image tag $JOB_NAME:v1.$BUILD_ID prabha442/$JOB_NAME:v1.$BUILD_ID '
	 sh ' docker image tag $JOB_NAME:v1.$BUILD_ID prabha442/$JOB_NAME:latest '

	 }
	}
    

      }
     } 
