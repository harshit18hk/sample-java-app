pipeline {
    
	agent any
	
	stages{
  
        stage('CODE ANALYSIS with SONARQUBE') {
          
		  

          steps {
            withSonarQubeEnv('sonarqube-server') {
		 sh '''mvn sonar:sonar \
                 -Dsonar.projectKey=test2 \
                 -Dsonar.host.url=http://3.14.145.21 '''
                
               }
            timeout(time: 10, unit: 'MINUTES') {
               waitForQualityGate abortPipeline: true
            }
          }
        }
  
  
  
  
  
  
  }
  
}
  
