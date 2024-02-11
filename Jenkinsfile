pipeline {
  agent any
  tools { 
        maven 'Apache-MAVEN'  
    }
   stages{
    stage('Compile and SAST Scanning') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=napasornss -Dsonar.organization=napasornss -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=7d4e4d14cc0c48a50aa34461f6ecf89d619c7911'
			}
    }

	stage('SCA Scanning') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
