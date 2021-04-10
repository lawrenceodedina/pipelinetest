pipeline{
  agent any
  tools{
    maven 'M2_HOME'
  }
  stages {
    stage('Build'){
      steps{
        sh 'mvn clean'
        sh 'mvn install'
        sh 'mvn package'
      }
    }
    stage('Test'){
      steps{
        echo "Test step"
        sh 'mvn test'
      }
    }
    stage('Deploy'){
      steps{
        script{
          checkout scm
          docker.withRegistry('', 'dockerID') {
          def customImage = docker.build("femiodedina/devops-pipe:${env.BUILD_ID}")
          def customImage1 = docker.build("femiodedina/devops-pipe")
          customImage.push()
          customImage1.push("latest")
        }
      }
    }
  }
