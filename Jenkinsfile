pipeline {
    agent any


    stages {
        stage('Clean Compile') {
            steps {
                
                // Clean and compile.
                sh "mvn clean compile"

            }
        }
        
        stage('Test') {
            steps {
                
                // Test Cases.
                sh "mvn test"

            }
        }
        
        stage('Install') {
            steps {
                
                
                sh "mvn install"

            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                // Analyzing code.
                withSonarQubeEnv('sonar'){
                    sh "mvn sonar:sonar"
                    }
            }
        }
        stage('Artifact'){
            steps{
                    archiveArtifacts 'target/*.war'
                }
            }
            
        stage ('Artifactory Configuration') {
            steps {
                rtServer (
                    id: "artifactory", 
                    url: "http://192.168.56.103:8081/artifactory",

                )

                rtMavenResolver (
                    id: 'maven-resolver',
                    serverId: 'artifactory',
                    releaseRepo: 'libs-release',
                    snapshotRepo: 'libs-snapshot'
                )  
                 
                rtMavenDeployer (
                    id: 'maven-deployer',
                    serverId: 'artifactory',
                    releaseRepo: 'libs-release-local',
                    snapshotRepo: 'libs-snapshot-local'
                )
            }
        }
        
        stage('upload') {
           steps {
              script { 
                 def server = Artifactory.server 'artifactory'
                 def uploadSpec = """{
                    "files": [{
                       "pattern": "/var/lib/jenkins/workspace/com.nagarro.pipeline.maven/target/mvc_1.war",
                       "target": "libs-snapshot-local"
                    }]
                 }"""

                 server.upload(uploadSpec) 
               }
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "artifactory"
                )
            }
        }
    }
}