pipeline {
   agent any
   environment {
	  registry = "ashwani00002/xebia_k8s"
	  registryCredential = 'DockerHub-Ashwani'
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
		
	        //sh 'cd ${NODEPATH}/src'
		//sh 'mkdir -p ${NODEPATH}/src/hello-world'
		// Copy all files in our Jenkins workspace to our project directory.
		//sh 'cp -r ${WORKSPACE}/* ${NODEPATH}/src/hello-world'
		sh 'npm install'
		//sh 'npm config ls'               
           }
       }
	   
	 }
	 
}
