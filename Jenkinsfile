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

    stage('Mail Notification') {
      steps {
        mail(subject: 'notification phase Build', body: 'cc', to: 'hk_hab_el_hames@esi.dz')
      }
    }

  }
}