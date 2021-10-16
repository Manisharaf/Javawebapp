pipeline {
    
    agent { label 'maven' }
    
    stages {
        
        stage('build') {
            steps {
                sh 'mvn clean install'            
            }
        }
        
        stage('Unit Testing junit')
        {
            steps
            {
                junit 'target/surefire-reports/*.xml'
            }
        }
        
        stage('Code Coverage')
        {
            steps
            {
            jacoco()
            }
        }
        
    }
}
