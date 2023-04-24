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
            //junit 'test-results/**/*.xml'
            echo "this will be test report"
        }
      }
    }
    
    stage('Deploy') {
      steps {
        sshagent(['my-creds']) {
          sh 'ssh -v -o StrictHostKeyChecking=no ubuntu@ec2-54-167-56-20.compute-1.amazonaws.com "rm -rf /var/www/html/*"'
          sh 'scp -o StrictHostKeyChecking=no -r build/ ubuntu@ec2-54-167-56-20.compute-1.amazonaws.com:/var/www/html/'
        }
      }
    }
  }
}
