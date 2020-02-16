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
	   
   }
	 
}
