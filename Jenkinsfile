pipeline {
  agent any

  stages {
    stage('Clone') {
      steps {
        git url: 'https://github.com/7etrahedral/jenkinsfile_repo.git', branch: 'main'
      }
    }

    stage('Build') {
      steps {
        echo 'Building the project...'
        // Example: sh 'make build' or npm install
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        // Example: sh 'npm test'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying...'
        // Example: sh './deploy.sh'
      }
    }
  }
}
