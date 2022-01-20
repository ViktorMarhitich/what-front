pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  tools {
    maven 'mv'
  }
  stages {
    stage('Scan') {
      steps {
        withSonarQubeEnv(installationName: 'sq') { 
          
          sh './mvnw clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
        }
      }
    }
  }
}
