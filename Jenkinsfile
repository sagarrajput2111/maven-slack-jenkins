pipeline {
  agent any
  stages {
    stage('Fetching code from github') {
          steps {
            git(url: 'https://github.com/sagarrajput2111/maven-slack-jenkins.git', branch: 'master', credentialsId: 'git_ssh_key')
          }
        }
    stage('generating artifacts') {
      
        
          steps {
            sh 'mvn clean install'
          }
    }

    stage('deploying code to tomcat') {
      steps {
        deploy(adapters: [tomcat9(credentialsId: 'tomcatpass', path: '', url: 'http://20.197.32.141:8081/')], war: '**/*war')
      }
    }

  }
  
}
