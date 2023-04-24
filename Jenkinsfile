pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/etechDevops/etech-mavenApp.git']]])
      }
    }
    stage('2-cleanws'){
      steps{
        sh 'mvn clean'
      }
    }
    stage('3-mavenbuild'){
      steps{
        sh 'mvn package'
      }
    }
    stage('unittest'){
        steps{
            sh 'mvn test'
        }
    }
    stage('sonarscanner'){
        steps{
       sh "mvn clean verify sonar:sonar\
  -Dsonar.projectKey=team5codereview\
  -Dsonar.projectName='team5codereview'\
  -Dsonar.host.url=http://ec2-54-84-57-138.compute-1.amazonaws.com:9000\
  -Dsonar.token=sqp_ef7bb738146ef3e44681754b0d4650034c10e221'
        }
    }
  }
}
