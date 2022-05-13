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
                    archiveArtifacts artifacts: '**/target/*.jar'
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
                 -Dsonar.projectName=jenkins-sonar-project \
                   -Dsonar.projectVersion=1.0 \
                 -Dsonar.host.url=http://172.31.13.247 '''
                
                  
                  
                 
	     }
		   timeout(time: 10, unit: 'MINUTES') {
               waitForQualityGate abortPipeline: true
            }
	  }
	}	
  
  
  
  
  
  
  }
  
}
  
