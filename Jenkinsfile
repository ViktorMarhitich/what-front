pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        
      }
    }
    stage('SonarQube analysis') {
      steps {
        script {
          def scannerHome = tool 'sonarscan';
          withSonarQubeEnv('sq') {
            sh "${tool("sonarscan ")}/bin/sonar-scanner -Dsonar.projectKey=reactapp -Dsonar.projectName=reactapp"
          }
        }
      }
    }
  }         
}
