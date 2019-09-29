pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
				git "https://github.com/m1m2m3/maven-project.git"
	         }
        }
        stage('Test') {
            steps {
           withMaven(jdk: 'myjdk', maven: 'mymaven')
					{
					sh 'mvn test'      
					}    
				}
        }
       
    }
}
