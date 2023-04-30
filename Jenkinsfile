pipeline {
   agent any
   environment {
       registry = '876724398547.dkr.ecr.ap-northeast-1.amazonaws.com/docker_project'
       
    }
   
   
    
    stages {
        stage('Build') {
            steps {
               // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }

           post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                     //step( [ $class: 'JacocoPublisher' ] )
                    archiveArtifacts '/target/*.war'
                }
            }
            
        }
        /*
        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven') {
                    sh 'mvn test'
                }
            }
        }
        
        stage ('Verify Stage'){
        
            steps {
                withMaven(maven : 'maven') {
                    sh 'mvn verify'
                }
            }
        }
        
        stage ('Package Stage'){
        
            steps {
                withMaven(maven : 'maven') {
                    sh 'mvn install'
                }
            }
        }
    }
