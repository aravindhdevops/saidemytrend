pipeline{
	agent any
	environment{
		PATH="/opt/maven/bin:$PATH"
        }
	stages{
		stage('build'){
			steps{
				sh 'mvn clean package'
			}
		}
		stage('SonarQube analysis'){
			environment{
				sonarqubePath= tool 'raj-sonarqube-scanner'
			}
			steps{
				withSonarQubeEnv('raj-sonarqube-server') {  
                    			sh "${scannerHome}/bin/sonar-scanner"  
                		}
			}
		}

	}
}
