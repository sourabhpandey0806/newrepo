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
    }
}
