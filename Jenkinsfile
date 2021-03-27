pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        powershell 'gradle build '
        powershell 'Gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
      }
    }

  }
}