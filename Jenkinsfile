pipeline{

      agent {
                docker {
                image 'maven'
		args '-v $HOME/.m2:/var/maven/.m2:z -e MAVEN_CONFIG=/var/maven/.m2 -e MAVEN_OPTS="-Duser.home=/var/maven"'

                }
            }
        
        stages{

              stage('Quality Gate Status Check'){
                  steps{
                      script{
			      withSonarQubeEnv('demo') { 
			      sh "mvn sonar:sonar \
 					 -Dsonar.projectKey=demo \
					  -Dsonar.host.url=http://54.174.121.17:9000 \
					  -Dsonar.login=dfdb5465652d729babebb76bf934a1ba8651de38"
                       	     	}
			      timeout(time: 1, unit: 'HOURS') {
			      def qg = waitForQualityGate()
				      if (qg.status != 'OK') {
					   error "Pipeline aborted due to quality gate failure: ${qg.status}"
				      }
                    		}
		    	   
			      
		  
                 	}
               	 }  
              }	
		
            }	       	     	         
}
