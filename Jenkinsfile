pipeline{
	agent {
		label 'green'
		}
	environment{
	JAVA_HOME = '/home/tom/project/jdk-11.0.21'
		}	
	stages{
		stage("Checkout"){
			steps{
			checkout scm
				}
			}
		stage("Build"){
			steps{
			  sh '/home/tom/project/apache-maven-3.9.6/bin/mvn install'					}
				}
		stage("Deployment"){
			steps{
			sh 'scp target/APPLE.war jerry@172.17.0.3:project/apache-tomcat-9.0.89/webapps'
				}
				   }	
		stage("Notification"){
			steps{
				slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#apple', color: 'grren', message: 'Build is successfull', teamDomain: 'DEVOPS', tokenCredentialId: 'apple', username: 'siri'
			}
				}
		}
	}
	
	
