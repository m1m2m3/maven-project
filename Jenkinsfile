pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
				git "https://github.com/m1m2m3/maven-project.git"
	         }
        }
        stage('Test')
	    {
            steps {
           withMaven(jdk: 'myjdk', maven: 'mymaven')
					{
					sh 'mvn test'      
					}    
		 }
            }
	  stage('Package')
	    {
            steps {
           withMaven(jdk: 'myjdk', maven: 'mymaven')
					{
					sh 'mvn package'      
					}    
		 }
            }
	    
	   stage('install')
	    {
            steps {
           withMaven(jdk: 'myjdk', maven: 'mymaven')
					{
					sh 'mvn install'      
					}    
		 }
            }
	   stage ('Deploy to Tomcat') 
	    {
	   steps{
           sshagent (['3.89.133.217']) {
           sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@3.89.133.217:/var/lib/tomcat/webapps'
                            }
                }
           }

 }
}
