pipeline {
  agent any
  environment {
   
    S3_BUCKET_NAME = 'jenkinsartifacts23'
  }
  

  
  stages {
    stage('Build') {
      steps {
        // Build the Maven project
        sh 'mvn clean package'
      }
    }
    
    stage('Publish') {
      steps {
        // Publish the artifact to S3
     
          s3Upload(entries.bucket: true, payloadSigningEnabled: true, bucket: "${S3_BUCKET_NAME}", .: './target': '**/*.war')
        
      }
    }
  }
}
