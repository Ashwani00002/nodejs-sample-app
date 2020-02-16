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
	 



	stage('Kubernetest_Deployment')  {

		    environment {
                    NVM_DIR="$HOME/.nvm"
                     when { branch "master" }
            	   }
             steps {
                 nvm(nvmInstallURL: "https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh",
                        nvmIoJsOrgMirror: "https://iojs.org/dist",
                        nvmNodeJsOrgMirror: "https://nodejs.org/dist",
                         version: "10.16.2") 
						{
                        echo '******Cloning Repo with TAGs ********'
			            }
                    }

				}

		stage('Remove Unused docker image') {
		steps
			{
			sh 'kubectl get svc'
			//echo '$IMAGE_ID'
			}
			}
			
			
			}
	 
	   	}
	
