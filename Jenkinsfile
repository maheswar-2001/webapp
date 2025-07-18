pipeline{
 tools{
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }
     agent any
	  
	  stages{
	  
	  stage("checkout"){
	   steps{
	   git 'https://github.com/maheswar-2001/webapp.git'
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

sshagent(['tomcatserver']) {
    // some block
sh """
scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@15.206.165.99:/home/ec2-user/tomcatserver/webapps/
ssh ec2-user@15.206.165.99/home/ec2-user/tomcatserver/bin/shutdown.sh
ssh ec2-user@15.206.165.99/home/ec2-user/tomcatserver/bin/startup.sh
          """
}
	   
		}
		  
	  }


	}
	}
