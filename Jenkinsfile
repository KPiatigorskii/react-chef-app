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
          sh """
          echo "${WORKSPACE}"
          ls -l
          ssh -o StrictHostKeyChecking=no ubuntu@ec2-3-83-182-36.compute-1.amazonaws.com "rm -rf /home/ubuntu/my-blog/*"
          scp -o StrictHostKeyChecking=no -r ${WORKSPACE}/my-blog  ubuntu@ec2-3-83-182-36.compute-1.amazonaws.com:/home/ubuntu/my-blog/
          """
        }
      }
    }

    stage('Deploy to develop') {
      when {
        branch 'develop'
      }
      steps {
        sshagent(['my-creds']) {
          sh """
          echo "${WORKSPACE}"
          ls -l
          ssh -o StrictHostKeyChecking=no ubuntu@ec2-3-83-182-36.compute-1.amazonaws.com "rm -rf /home/ubuntu/my-blog-develop/*"
          scp -o StrictHostKeyChecking=no -r ${WORKSPACE}/my-blog  ubuntu@ec2-3-83-182-36.compute-1.amazonaws.com:/home/ubuntu/my-blog-develop/
          """
        }
      }
    }
    
    stage('Deploy to master') {
      when {
        branch 'master'
      }
      steps {
        sshagent(['my-creds']) {
          sh """
          echo "${WORKSPACE}"
          ls -l
          ssh -o StrictHostKeyChecking=no ubuntu@ec2-3-83-182-36.compute-1.amazonaws.com "rm -rf /home/ubuntu/my-blog-master/*"
          scp -o StrictHostKeyChecking=no -r ${WORKSPACE}/my-blog  ubuntu@ec2-3-83-182-36.compute-1.amazonaws.com:/home/ubuntu/my-blog-master/
          """
        }
      }
    }
  }
}
