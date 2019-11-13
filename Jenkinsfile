pipeline{
    agent any
    stages{
        
        stage('Build'){
            steps('Maven package'){
                    def mvnHome = tool name: 'maven-3.6.2', type: 'maven'
                    def mvnCMD = "$mvnHome/bin/mvn"
                    sh label: '', script: "$mvnCMD clean package"
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
