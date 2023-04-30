pipeline {
  agent any
  

  
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
     
          s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, bucket: "${jenkinsartifacts23}", workingDir: './target', glob: '**/*.war')
        
      }
    }
  }
}
