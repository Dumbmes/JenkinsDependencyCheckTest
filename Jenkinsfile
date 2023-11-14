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
        dependencyCheck additionalArguments: '--format HTML --format XML --suppression suppression.xml', odcInstallation: 'Plswork'
      }
    }
  }  
  post {
    success {
      dependencyCheckPublisher pattern: 'dependency-check-report.xml'
    }
  }
}
