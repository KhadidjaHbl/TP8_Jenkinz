pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        powershell 'gradle build'
        powershell 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar, build/docs/javadoc/*'
      }
    }

    stage('Mail Notification') {
      post {
        failure {
          mail(subject: 'notification phase Build', body: 'Le build est execute avec echec ', to: 'hk_hab_el_hames@esi.dz')
        }

        success {
          mail(subject: 'notification phase Build', body: 'Le build est execute avec succes ', to: 'hk_hab_el_hames@esi.dz')
        }

      }
      steps {
        powershell 'send email '
      }
    }

  }
}