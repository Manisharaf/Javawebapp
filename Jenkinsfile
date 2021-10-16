pipeline {
    agent { label 'maven' }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean install'            
            }
        }
    }
}
