pipeline {
  agent any
  stages {
    stage('Checkout SCM') {
      steps {
        git '/home/Documents/GitHub/JenkinsDependencyCheckTest'
      }
    }

    stage('OWASP DependencyCheck') {
      steps {
        dependencyCheck additionalArguments: '--format HTML --format XML --suppression suppression.xml', odcInstallation: 'Default'
      }
    }
	
	stage('Code Quality Check via SonarQube'){
		steps {
			script {
				def scannerHome = tool 'SonarQube';
					withSonarQubeEnv('SonarQube'){
						sh "${scannerHome}/bin/sonar-scanner \
							-Dsonar.projectKey=OWASP \
							-Dsonar.sources=. \
							-Dsonar.host.url=http://172.18.0.4:9000 \
							-Dsonar.token=sqp_71cc3f295208b71469c1284bb322a4a14c880e62"
					}
				}
			}
		}	
  }  
  post {
	
    success {
      dependencyCheckPublisher pattern: 'dependency-check-report.xml'
    }
  }
}
