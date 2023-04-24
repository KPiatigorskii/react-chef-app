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
          sh '''ssh -v -o StrictHostKeyChecking=no ubuntu@ec2-3-83-182-36.compute-1.amazonaws.com "rm -rf /home/ubuntu/my-blog/*"'
                scp -o StrictHostKeyChecking=no -r * ubuntu@ec2-3-83-182-36.compute-1.amazonaws.com:/home/ubuntu/my-blog/'''
        }
      }
    }
  }
}
