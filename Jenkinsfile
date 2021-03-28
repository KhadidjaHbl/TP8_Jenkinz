pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'C:\\Users\\Home\\Downloads\\gradle-5.6\\bin\\gradle build'
        bat 'C:\\Users\\Home\\Downloads\\gradle-5.6\\bin\\gradle javadoc'
        archiveArtifacts 'build/libs/*.jar, build/docs/javadoc/*'
      }
    }

    stage('Mail Notification') {
      steps {
        powershell 'gradle javadoc'
      }
    }

  }
}