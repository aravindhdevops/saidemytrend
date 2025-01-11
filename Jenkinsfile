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

	}
}
