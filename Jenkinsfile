pipeline {
  agent any
  stages {
    stage('\'Dev-Build') {
      steps {
        git(url: 'https://github.com/KishoreTJ/WebApp.git', branch: 'master', poll: true)
        bat 'start /min stopApp.bat'
        bat ' maven C:\\apache-maven-3.8.5-bin\\apache-maven-3.8.5'
        bat 'mvn install'
        bat 'Set JENKINS_NODE_COOKIE=dontKillMe && start /min startApp.bat'
      }
    }

    stage('Test Automation') {
      parallel {
        stage('Test Automation') {
          steps {
            echo 'Test Automation'
          }
        }

        stage('QA UI Automation') {
          steps {
            git(url: 'https://github.com/KishoreTJ/WebAppUiAutomation.git', poll: true)
            sleep 10
            bat 'mvn test'
          }
        }

        stage('QA API Automation') {
          steps {
            git(url: 'https://github.com/KishoreTJ/WebAppApiAutomation', branch: 'master', poll: true)
            sleep 10
            bat 'mvn test'
          }
        }

      }
    }

  }
}