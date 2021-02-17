node{
  stage('SCM Checkout'){
	  git branch: 'wartomcat', url: 'https://github.com/abdulw786/devopsprojects.git'
  
	}
  
  stage('Compile-Package'){
	 def mvnHome = tool name: 'apache-maven-3.6.3', type: 'maven'
  	 sh "${mvnHome}/bin/mvn package"
	}
	
	
	stage('Deploy to Tomcat'){
		sshagent(['ec2jenkins.pem']) {
		sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@34.227.56.240:/opt/tomcat9/webapps/'
	}
  
}
