pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Hello World'
      }
    }

    stage('Deploy') {
      steps {
        input(message: 'Should we continue?', submitter: 'admin')
      }
    }

  }
}