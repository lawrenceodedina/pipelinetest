pipeline{
  agent any
  tools{
    maven 'M2_HOME'
  }
  environment{
    registry = "femiodedina/devops-pipe"
    registryCredential= 'dockerID'
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
          docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
  }
}
