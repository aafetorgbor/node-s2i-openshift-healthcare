pipeline{
    
    agent any
    
    environment{
        
        scannerhome = tool 'SonarQubeScanner'
        
    }
    
    stages{
        stage('Checking out source code'){
            steps{
               checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/aafetorgbor/node-s2i-openshift-healthcare.git']]])
            }
        }
        
       
        
 
        
        stage('SonarQube Analysis Check'){
            steps{
                
               script {
                  // SonaQube server name from jenkins and sonarqube project name
                   withSonarQubeEnv('sonarqube') {
                     sh "$scannerhome/bin/sonar-scanner -Dsonar.projectKey=advanced -Dsonar.projectName=advanced"
                   }
               }
            }
           
        }
        
        
        stage("Quality Gate Validation") {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                  waitForQualityGate abortPipeline: true
                }
            }
        }
        
        
        
        
        
          
    }
    
}
