pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        powershell 'gradle build '
        powershell 'Gradle javadoc'
      }
    }

  }
}