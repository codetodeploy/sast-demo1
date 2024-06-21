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
      
      stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }

    stage('Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                 script{
                 app =  docker.build("skabhi003")
                 }
               }
            }
    }

	stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://268285888909.dkr.ecr.ap-south-1.amazonaws.com/', 'ecr:ap-south-1:aws-credentials') {
                    app.push("latest")
                    }
                }
            }
    	}		
  }
}
