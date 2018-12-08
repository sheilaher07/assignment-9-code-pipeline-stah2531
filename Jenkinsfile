pipeline {
   agent {label 'linux'}
   stages {
      stage('Unit Tests') {  
         steps {
            sh 'ant -f test.xml -v'
            junit 'reports/result.xml'  
         }
      }   
      stage('Build') {   
         steps {
            sh 'ant -f build.xml -v'   
         }
      }   
      stage('Deploy') {    
         steps {
            sh 'aws s3 cp /workspace/java-pipeline/dist/ s3://stah2531-assignment-9/ --recursive --include "rectangle-${BUILD_NUMBER}.jar"'
         }
      }
   }
}
