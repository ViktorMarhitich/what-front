pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        
      }
    }
    stage('Code Quality Check via SonarQube') {
    steps {
       script {
       def scannerHome = tool 'sq';
           withSonarQubeEnv("sq") {
           sh "${tool("sq")}/bin/sonar-scanner \
           -Dsonar.projectKey=test-node-js \
           -Dsonar.sources=. \
           -Dsonar.css.node=. \
           -Dsonar.host.url=http://18.159.109.85:9000 \
           -Dsonar.login=47b3d4a91136ef824c21ab197621d3fdeb7d55fd"
               }
           }
       }
    }
  }         
}
