pipeline {
   agent {label 'linux'}
   stages {
      stage('Unit Tests') {  
         steps {
            git 'https://github.com/stah2531/java-project.git'
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
            withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '67608e55-6f33-49ae-843e-973d9197f77a', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins" 
            }
         }
      }
   }
}
