pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        powershell './gradlew build'
        powershell 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar, build/docs/javadoc/*'
        bat 'gradle build'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(to: 'hk_hab_el_hames@esi.dz', subject: 'gradle build', body: 'the result of build is : ${currentBuild.result}')
      }
    }

  }
}