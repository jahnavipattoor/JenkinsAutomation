pipeline {
  agent any
  stages {
    stage('Dev-Build') {
      steps {
        git(branch: 'master', poll: true, url: 'https://github.com/TestLeafInc/WebApp.git')
        bat 'mvn install'
        bat 'Start App.bat'
        bat 'Stop App.bat'
      }
    }

    stage('UI-Automation') {
      parallel {
        stage('UI-Automation') {
          steps {
            git(url: 'https://github.com/TestLeafInc/WebAppUiAutomation.git', poll: true, branch: 'master')
            bat 'mvn test'
          }
        }

        stage('API-Automation') {
          steps {
            git(url: 'https://github.com/TestLeafInc/WebAppApiAutomation.git', branch: 'master', poll: true)
            bat 'mvn test'
          }
        }

        stage('Performance testing') {
          steps {
            echo 'Jmeter testing done'
          }
        }

      }
    }

    stage('UAT Testing') {
      steps {
        echo 'UAT done'
      }
    }

    stage('Prod') {
      steps {
        input 'Can I deploy to prod'
      }
    }

  }
}