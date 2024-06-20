pipeline {
  agent any
  tools { 
        maven 'mymaven'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=mylw-test -Dsonar.organization=mylw-test -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=594aca8fb761f5dfc7ec96f200b98c3b527491cc'
			}
        } 
  }
}
