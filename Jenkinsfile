pipeline 
{ 
agent any
   {
     stage "SCM checkout"
	{
	git "https://github.com/m1m2m3/maven-project.git"
         }	  
     stage "Code Test"
	{
	withMaven(jdk: 'myjdk', maven: 'mymaven')
	      {
	    sh 'mvn test'      
        	}
		
	}
	
  }
}
