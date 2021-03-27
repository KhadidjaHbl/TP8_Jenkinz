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
        emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n",
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
      }
      steps {
        powershell 'send email '
      }
    }

  }
}
