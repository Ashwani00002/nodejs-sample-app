/*
###############################################################################
Jenkinsfile Name: Jenkinsfile
Project         : Teamster 213 Backend (Nodejs)
Description     : This jenkinsfile is used for implementing CI/CD of this project.
Jenkins URL     : https://jenkins.celestialsys.tk
Maintainers     : Ashwani Verma(Celestial DevOps Team)
Email           : a.verma@celestialsys.com
Disclaimer      : Any modification in this file should be done after consultation
                  with the DevOps Team.
###################################################################################
*/

pipeline {
   agent any
   environment {
	  registry = "ashwani00002/xebia_k8s"
	  registryCredential = 'Docker_Hub'
	  dockerImage = ''
   }
   stages {
       stage('Build') {
	     agent {
               docker {
                   image 'node:10-alpine'
               }
           }
           steps {
		sh 'ls -la && pwd'
		sh 'npm install'
		sh 'npm config ls' 
		sh 'cat package.json'
           }
        }

	   
	   
      stage('Test') {
           agent {
               docker {
                   image 'node:10-alpine'
               }
           }
           steps {
               sh 'echo Running Unit Tests'
               sh 'npm test'
           }
       }
	   
	
    stage('Building image') {
      steps {
        script {
          	dockerImage = docker.build registry + ":$BRANCH_NAME.$BUILD_NUMBER"
        }
      }
	 }  
	   
	   
	       stage('Deploy Image to DockerHub') {
      steps {
      	script {
        	echo 'Deploying docker images in DockerHub'
        	docker.withRegistry( '', registryCredential ) 
            {
            dockerImage.push()
            }
          }
    	 }
     }
	 
   stage('DELETING DANGLING IMAGES') {	
     steps {	
	   script {
	    	
	    	echo 'DELETING DANGLING IMAGES'
	    	sh '''docker images'''
	    	sh '''docker rmi -f $(docker images | grep "master" | awk '{print $1 ":" $2}')'''
	    
	    	}
      	  }
    }


	   stage('Kubernetes_Deployment') {
	   	agent {label 'MINIKUBE'}
		 when { branch "master" }
	   	steps
			{
			sh 'kubectl get svc'
			sh 'kubectl get deploy -o=wide'
			sh 'kubectl set image deployment/xebia-deployment xebia-container=ashwani00002/xebia_k8s:"$BRANCH_NAME.$BUILD_NUMBER" '
			sh 'kubectl get deploy -o=wide'
			}
			}
	   
			
	   
  stage('Send Notification')
  	{
          steps {
  			echo ' Sending Notification EMAIL ....'
  		}
  	  post 
  	   {
    	   always {
              emailext (
		      
              		subject: "Job '${env.JOB_NAME} branch ${env.BUILD_NUMBER}'",
		      
              		body: """Check console output at "${env.BUILD_URL}" ${env.JOB_NAME}. 
	      			App is runnig at -->   http://3.6.243.217:32000/
	      			""",
		      
              		to: "ashwaniverma00002@gmail.com",
              		from: "ashwaniverma0002@gmail.com")
        }
      }
    }
} 
	post {
    success {

      emailext (
          subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                   Check console output at "${env.BUILD_URL}"
                """,
          to: "ashwaniverma00002@gmail.com",
          from: "ashwaniverma0002@gmail.com" )
       
    }

    failure {

      emailext (
          subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                 Check console output at "${env.BUILD_URL}"            
                """,
          to: "ashwaniverma00002@gmail.com",
          from: "ashwaniverma0002@gmail.com" )
		}
	}
 
}
	
