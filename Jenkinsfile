node {
  stage('Checkout Source Code') {
    checkout scm
  }
  stage('Run SonarQube Analysis') {
    def scannerHome = tool 'SonarQubeScanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
