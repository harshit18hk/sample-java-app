pipeline {
    
	agent any
	
	tools {
        maven "maven"
    }
	
	stages{
  
        stage('CODE ANALYSIS with SONARQUBE') {
          
		  

          steps {
            withSonarQubeEnv('sonarqube-server') {
		 sh '''mvn sonar:sonar \
                 -Dsonar.projectKey=test2 \
                 -Dsonar.host.url=http://3.15.223.197 '''
                
               }
            timeout(time: 10, unit: 'MINUTES') {
               waitForQualityGate abortPipeline: true
            }
          }
        }
  
  
  
  
  
  
  }
  
}
  
