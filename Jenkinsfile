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
   agent {label 'K8S_SLAVE'}
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
			steps {
				nvm(nvmInstallURL: "https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh",
                nvmIoJsOrgMirror: "https://iojs.org/dist",
                nvmNodeJsOrgMirror: "https://nodejs.org/dist",
                version: "10.16.2") 
				{
                sh 'echo $GIT_BRANCH'
				echo '********Running NPM Install **********'
				sh 'npm install'
				}
			}
		}
	}
}
