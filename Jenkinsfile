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
        powershell 'send email '
      }
       post {
            failure {
                mail(subject: 'notification phase Build', body: 'Le build est éxécuté avec échec ', to: 'hk_hab_el_hames@esi.dz')}
            success {
                mail(subject: 'notification phase Build', body: 'Le build est éxécuté avec succés ', to: 'hk_hab_el_hames@esi.dz')}
      }
  }

  }
}
