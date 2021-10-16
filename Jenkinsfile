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
        
        stage('Code Quality Check (Sonarqube)')
        {
            environment {
                projectKey = 'Javawebapp'
                projectName = 'Javawebapp'
                projectVersion = '1.1'
                sonarSources = 'src'
                sonarLanguage = 'java'
                sonarBinaries = 'target/classes'
                sonarCoverageformat = '-Dsonar.coverage.jacoco.xmlReportPaths'
                coverageReportPath = 'target/jacoco.xml'
                sonarSourceEncoding = 'UTF-8'                
            }
            steps
            {
                script
                {
                    def sonarscanner = tool'sonar_scanner'
                    withSonarQubeEnv('sonarqube') {
                        sh """
                        ${sonarscanner}/bin/sonar-scanner -Dsonar.projectKey=${projectKey} \
                            -Dsonar.projectName=${projectName} \
                            -Dsonar.projectVersion=${projectVersion} \
                            -Dsonar.sources=${sonarSources} \
                            -Dsonar.language=${sonarLanguage} \
                            -Dsonar.java.binaries=${sonarBinaries} \
                            ${sonarCoverageformat}=${coverageReportPath} \
                            -Dsonar.c.file.suffixes=- \
                            -Dsonar.cpp.file.suffixes=-\
                            -Dsonar.objc.file.suffixes=- \
                            -Dsonar.sourceEncoding=${sonarSourceEncoding}
                        """                    
                    }
                }
            }
        
        }
        
    }
}
