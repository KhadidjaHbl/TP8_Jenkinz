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
        mail(to: 'hk_hab_el_hames@esi.dz', subject: "status of build: ${currentBuild.fullDisplayName}", body: "${env.BUILD_URL} has result ${currentBuild.currentResult}")
      }
    }

    stage('Code Analysis') {
          steps {
            withSonarEnv('SonarQube'){bat "gradlew sonarqube"
                }
          script {
              def qualitygate= waitForQualityGate()
              if (qualitygate.status != "OK") {error "Pipeline aborted : ${qualitygate.status}"}
          }
       }
     }
 }
}
