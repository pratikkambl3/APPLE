pipeline{
	agent {
		label 'green'
		}
	environment{
	JAVA_HOME = '/home/tom/project/jdk-11.0.21'
		}
	parameters {
  choice choices: ['QA', 'UAT', 'PROD'], name: 'ENV'
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
			sh '''if [ $ENV = "QA" ];then
echo "DEPLOYED TO QA"
cp target/APPLE.war /home/tom/project/apache-tomcat-9.0.89/webapps
elif [ $ENV = "UAT" ];then
echo "DEPLOYED TO UAT"
scp target/APPLE.war jerry@172.17.0.3:project/apache-tomcat-9.0.89/webapps
elif [ $ENV = "PROD" ];then
echo "DEPLOYED TO PROD"
scp target/APPLE.war pratikkambl3@172.17.0.1:/home/pratikkambl3/Documents/Devops-Tools/apache-tomcat-9.0.89/webapps
				fi'''
				
				}
				   }	
		stage("Notification"){
			steps{
				slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#apple', color: 'grren', message: 'Build is successfull', teamDomain: 'DEVOPS', tokenCredentialId: 'apple', username: 'siri'
			}
				}
		}
	}
	
	
