pipeline{
	tools{
		jdk 'JAVA_HOME'
		maven 'M2_HOME'
	}
	agent any
	stages{
		stage("git checkout"){
			steps{
			git 'https://github.com/swadhinswain475/webapp-tomcat-deploy.git'
			}
		}
		
		stage("maven package"){
			steps{
			 sh 'mvn clean package'
			 sh 'mv target/*.war target/mywebapp.war'
			}
		}
		
		stage("tomcat deploy"){
			steps{
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
}
