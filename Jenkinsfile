pipeline{
 tools{
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
     agent any
	  
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git 'https://github.com/satapathytanmay/webapp.git'
	   }
	                  }
	
	   stage("compile"){
	    steps{
		 sh 'mvn compile'
		}
		}
       stage("test"){
	    steps{
		 sh 'mvn test'
		}
		}
       stage("package"){
	    steps{
		 sh 'mvn clean package'
                 sh "mv target/*.war target/myweb.war"

		}
		}
		  
      stage("deploy"){
	    steps{
		 sshagent(['TomcatServer']) {
    // some block
	sh """
                 
            scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@16.171.26.246:/home/ec2-user/tomcat10/webapps/

              ssh ec2-user@16.171.26.246/home/ec2-user/tomcat10/bin/shutdown.sh
              ssh ec2-user@16.171.26.246 /home/ec2-user/tomcat10/bin/startup.sh
            
          
          """



    // some block
}
}
        
		}
		}
	  }
