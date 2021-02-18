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
	stage('Slack Notification'){
	slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#jenkins', color: '#439FE0', message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}", tokenCredentialId: 'slack'
	
	}

stage('Email Notification'){
	mail bcc: '', body: 'build success done', cc: '', from: 'whashoory2gmail.com', replyTo: 'awhashoory@gmail.com', subject: 'build success by wahid', to: 'awhashoory@gmail.com'
	}
  
}
