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
	    
	   stage('SonarQube analysis') 
	    {
            steps {
            withSonarQubeEnv(credentialsId: 'abc', installationName: 'MySonar') 
	           {
                  sh 'mvn sonar:sonar'   // some block
                   }
      
               }
           }
	    
	   stage ('Deploy to Tomcat') 
	    {
	   steps{
           sshagent (['54.175.245.41']) {
           sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@54.175.245.41:/var/lib/tomcat/webapps'
                            }
                }
           }

 }
}
