pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/enwokocha/etech-mavenApp.git']]])
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
    stage('codequality'){
        steps{
       sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team6codereview \
  -Dsonar.projectName='team6codereview' \
  -Dsonar.host.url=http://ec2-3-136-87-213.us-east-2.compute.amazonaws.com:9000 \
  -Dsonar.token=sqp_9749d98725d8791a32d9d0088fb40cb887eb9611'
        }
    }
  }
}