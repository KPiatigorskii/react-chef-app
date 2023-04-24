pipeline {
  agent any
  
  stages {    
    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }
    
    stage('Run tests') {
      steps {
        sh 'npm run test'
      }
      post {
        always {
          junit 'test-results/**/*.xml'
        }
      }
    }
    
    stage('Deploy') {
      steps {
        echo 'Deploy stuff'
      }
    }
  }
}
