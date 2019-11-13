pipeline{
    agent any
    stages{
        
        stage('Build'){
            
            steps{
                withMaven(maven: 'maven-3.6.2'){
                    
                    sh 'mvn clean package'
                }

            }

        }
        stage('Deploy'){
            
            steps{
                
                withCredentials([ [ $class		: 'UsernamePasswordMultiBinding',
                					credentialsId	: 'PCF_USER',
                					usernameVariable: 'USERNAME',
                					passwordVariable	: 'PASSWORD']  ]){
                					                	 	                
                					   sh '/usr/local/bin/cf login -a http://api.run.pivotal.io -u $USERNAME -p $PASSWORD'             	 	                
                					   sh '/usr/local/bin/cf push'             	 	            
        		    }

    		    }

    		}

    }
}
