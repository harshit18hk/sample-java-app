pipeline {
    
	agent any
	
	tools {
        maven "maven"
    }
	
		
    stages{
        
        stage('BUILD'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

	stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

	stage('INTEGRATION TEST'){
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
		
        stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }

        stage('CODE ANALYSIS with SONARQUBE') {
          
		  

          steps {
            withSonarQubeEnv('sonarqube-server') {
		 sh '''mvn sonar:sonar \
                 -Dsonar.projectName=test \
                   -Dsonar.projectVersion=1.0 \
                 -Dsonar.host.url=http://18.117.189.117 '''
                
                  
                  
                 
	     }
		   timeout(time: 10, unit: 'MINUTES') {
               waitForQualityGate abortPipeline: true
            }
	  }
	}	
  
  
  
  
  
  
  }
  
}
  
