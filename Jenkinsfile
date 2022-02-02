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
    stage('Code Quality Check via SonarQube') {
    steps {
       script {
       def scannerHome = tool 'sq';
           withSonarQubeEnv("sq") {
           sh "${tool("sq")}/bin/sonar-scanner \
           -Dsonar.projectKey=test-node-js \
           -Dsonar.sources=. \
           -Dsonar.css.node=. \
           -Dsonar.host.url=http://62.171.182.32:9000 \
           -Dsonar.login=15373bb1f498a29ede21cacd687bb105dec45d1f"
               }
           }
       }
    }
    
    stage('Upload to S3'){
      steps {
        withAWS(credentials:'myaws'){
          s3Upload(file:'dist', bucket:'what-front', path:'/var/lib/jenkins/workspace/whatfornt_master/dist/') 
        }
      }
    }
  }         
}
