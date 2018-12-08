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
      stage('Report') {
         steps {
            withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '3a19bfb0-d79f-4eec-820d-cf236c2b226e', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins" 
            }
         }
      }
   }
}
