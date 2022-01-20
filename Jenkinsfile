pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        sh 'npm run build'
      }
    }  
    
    stage('SonarScan') {
      steps {
        withSonarQubeEnv('sq'){
          sh 'npm install sonar-scanner'
          sh 'npm run sonar'
        }
      }
    }        
    
  }
}
