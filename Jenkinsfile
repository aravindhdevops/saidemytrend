pipeline{
	agent any
	environment{
		PATH="/opt/maven/bin:$PATH"
        }
	stages{
		stage('build'){
			steps{
				sh 'mvn clean package -Dmaven.test.skip=true'
			}
		}
		stage('test'){
			steps{
				sh 'mvn surefire-report:report'
			}
		}
		stage('SonarQube analysis'){
			environment{
				scannerHome= tool 'raj-sonarqube-scanner'
			}
			steps{
				withSonarQubeEnv('raj-sonarqube-server') {  
                    			sh "${scannerHome}/bin/sonar-scanner"  
                		}
			}
		}
		 stage("Quality Gate") {   
            steps {                           
                script {                      
                    timeout(time: 1, unit: 'HOURS') {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            echo "Warning: Quality gate failed but continuing pipeline: ${qg.status}"
                        }
                    }
                }                             
            }                                
        } 

	}
}
