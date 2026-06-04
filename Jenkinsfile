pipeline{
	tools{
		jdk 'JAVA_HOME'
		mvn 'MAVEN_HOME'
	}
	
	agent any
	
	stages{
		stage{
			step("git checkout")
			 git branch: 'master',
			     url: https://github.com/swadhinswain475/webapp-tomcat-deploy.git
		}
		
		stage{
			step("maven package")
			 sh 'mvn clean package'
			  sh 'mv target/*.war target/mywebapp.war'
		}
		
		stage{
			step("tomcat deploy")
			 sshagent(['tomcat']) {
    // some block
	
	sh """
		scp -o StrictHostKeyChecking=no target/mywebapp.war ubuntu@43.205.213.247:/home/ubuntu/tomcat/webapps
		
		ssh ubuntu@43.205.213.247 /home/ubuntu/tomcat/bin/shutdown.sh
		ssh ubuntu@43.205.213.247 /home/ubuntu/tomcat/bin/startup.sh
	
	"""
}
		}
	}
}
