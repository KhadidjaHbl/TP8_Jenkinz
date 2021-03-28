pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar, build/docs/javadoc/*'
        bat 'C:\\Users\\Home\\Downloads\\gradle-5.6\\bin\\gradle build'
      }
    }

    stage('Mail Notification') {
      steps {
        powershell 'gradle javadoc'
      }
    }

  }
}