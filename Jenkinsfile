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
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh "exit 1"
            }
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
