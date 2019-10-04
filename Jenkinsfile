pipeline {
    agent any

    stages {
        stage('SCM Checkout') 
	    {
            steps {
		  git "https://github.com/m1m2m3/maven-project.git"
	          }
            }
        
           stage('build && SonarQube analysis') 
	    {
            steps {
                withSonarQubeEnv(credentialsId: 'sonar', installationName: 'Sonar') 
		    {
                    // Optionally use a Maven environment you've configured already
                 withMaven(jdk: 'myjdk', maven: 'mymaven') 
			    {
                        sh 'mvn clean package sonar:sonar'
                            }
                   }
                }
           }
	    
	   stage ('Deploy to Tomcat') 
	    {
	   steps{
           sshagent(['18.212.174.31']) 
		   {
                   sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@18.212.174.31:/var/lib/tomcat/webapps'
                    }
                }
           }

 }
}
