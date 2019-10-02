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
                withSonarQubeEnv(credentialsId: 'sonarnew', installationName: 'Sonar') 
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
           sshagent(['3.93.241.158']) 
		   {
                   sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@3.93.241.158:/var/lib/tomcat/webapps'
                    }
                }
           }

 }
}
