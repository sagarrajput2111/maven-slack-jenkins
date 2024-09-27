pipeline {
  agent any
  stages {
    stage('Fetching code from github') {
      parallel {
        stage('Fetching code from github') {
          steps {
            script {
              slackSend color: '#439FE0', message: "Starting build ${env.JOB_NAME} #${env.BUILD_NUMBER}..."
            }

            git 'https://github.com/sagarrajput2111/Maven-build-jenkins.git'
          }
        }

        stage('fetching code') {
          steps {
            git(url: 'https://github.com/sagarrajput2111/maven-slack-jenkins.git', branch: 'master', credentialsId: 'githubmaven')
          }
        }

      }
    }

    stage('generating artifacts') {
      parallel {
        stage('generating artifacts') {
          steps {
            sh 'mvn clean install'
          }
        }

        stage('build with maven') {
          steps {
            echo 'building'
          }
        }

      }
    }

    stage('deploying code to tomcat') {
      steps {
        deploy(adapters: [tomcat9(credentialsId: 'tomcatcreds', path: '', url: 'http://20.197.32.111:8081/')], war: '**/*war')
      }
    }

  }
  post {
    success {
      slackSend(color: 'good', message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} is successful!")
    }

    failure {
      slackSend(color: 'danger', message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} has failed!")
    }

    unstable {
      slackSend(color: 'warning', message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} is unstable!")
    }

    aborted {
      slackSend(color: 'danger', message: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} has been aborted!")
    }

  }
}