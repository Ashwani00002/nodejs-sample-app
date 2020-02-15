/*
###############################################################################
Jenkinsfile Name: Jenkinsfile
Project         : Xebia
Description     : This jenkinsfile is used for implementing CI/CD of this project.
Jenkins URL     : https://jenkins.celestialsys.tk
Maintainers     : Ashwani Verma(Celestial DevOps Team)
Email           : a.verma@celestialsys.com
Disclaimer      : Any modification in this file should be done after consultation
                  with the DevOps Team.
###################################################################################
*/

pipeline {
   agent {label 'K_Master'}
   environment {
	  NVM_DIR="$HOME/.nvm"
	  registry = "ashwani00002/xebia_k8s"
	  registryCredential = 'DockerHub-Ashwani'
	  dockerImage = ''
      }

    stages {
      stage('Pre-build setup') {
            steps {
					checkout scm
					}
				}

       stage('Build') {
           agent {
			dockerfile {
			filename 'Dockerfile'
				}
			}

		}
	}
}
