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
	  
    stage ( 'docker container deployment' ){
       steps {
	       def docker_run= ' docker run -itd --name webapp prabha442/jenkins-docker-project-1 '
	       def docker_rm_container= ' docker rm -f webapp '
               def docker_rmi= ' docker rmi -f prabha442/jenkins-docker-project-1 '
	       
	    sshagent(['ssh-agent']) {
		    sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.34.203 ${docker_rm_container}"
		    sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.34.203 ${docker_rmi}"
		    sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.34.203 ${docker_run}"
             }
          }
       }
    

      }
     } 
