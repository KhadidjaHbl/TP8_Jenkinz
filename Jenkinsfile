pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        powershell 'gradle build'
        powershell 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar, build/docs/javadoc/*'
        bat 'C:\\Users\\Home\\Downloads\\gradle-5.6\\bin\\gradle build'
      }
    }

    stage('Mail Notification') {
      steps {
        def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        def summary = "${subject} (${env.BUILD_URL})"
        def details = """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>"""
         emailext (
         subject: subject,
         body: details,
         recipientProviders: [[$class: 'DevelopersRecipientProvider']]
    )
      }
    }

  }
}
