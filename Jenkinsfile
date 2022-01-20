pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        
        withSonarQubeEnv('sq'){
          sh 'npm install sonar-scanner'
          sh 'npm run sq'
        }
      }
    }         
  }
}
