pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				echo '/home/JenkinsDependencyCheckTest'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				dependencyCheck additionalArguments: ''' 
                    -o './'
                    -s './'
                    -f 'ALL' 
                    --prettyPrint''', odcInstallation: 'Default'
        
        dependencyCheckPublisher pattern: 'dependency-check-report.xml'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}
