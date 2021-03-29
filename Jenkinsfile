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
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('SonarQube') {bat 'C:\\Users\\Home\\Downloads\\gradle-5.6\\bin\\gradle sonarqube'}

            script {
              echo "test2"
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {error "Pipeline aborted due to quality gate failure: ${qg.status}"}
              }
            }
          }
        }
      }

      stage('Test Reporting') {
        steps {
          cucumber 'reports/*.json'
        }
      }

      stage('Deployment') {
        steps {
          bat 'C:\\Users\\Home\\Downloads\\gradle-5.6\\bin\\gradle publish'
        }
      }

      stage('Slack Notification') {
        steps {
          slackSend(baseUrl: 'https://hooks.slack.com/services/', token: 'T01N51K5L01/B01SK5ZK7HT/8g4ZsGtZIBvn64iN5jzsefbu', channel: 'tpGradle', message: 'deployment finished', teamDomain: 'tpgradle-workspace.slack.com')
        }
      }
    }
  }
