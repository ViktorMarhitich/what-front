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
       catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh 'npm run test'
              }
       script {
       def scannerHome = tool 'sq';
           withSonarQubeEnv("sq") {
           sh "${tool("sq")}/bin/sonar-scanner \
           -Dsonar.projectKey=test-node-js \
           -Dsonar.sources=. \
           -Dsonar.css.node=. \
           -Dsonar.host.url=http://62.171.182.32:9000 \
           -Dsonar.login=15373bb1f498a29ede21cacd687bb105dec45d1f \
           -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info"
               }
           }
       }
    }
    
    stage('Upload to S3'){
      steps {
        withAWS(credentials:'myaws'){
          s3Upload(file:'dist', bucket:'what-front', path:'') 
        }
      }
    }
    
    stage('Invalidate Cloudfront'){
      steps {
        withAWS(credentials:'myaws'){
          cfInvalidate(distribution:'E36WF0UA7OUCJC', paths:['/*']) 
        }
      }
    }
  }         
}
