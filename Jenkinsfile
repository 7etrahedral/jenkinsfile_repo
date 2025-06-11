pipeline {
  agent any

  stages {
    stage('Clone') {
      steps {
        git url: 'https://github.com/7etrahedral/jenkinsfile_repo.git', branch: "main"
      }
    }

    stage('Build') {
      steps {
        echo 'Building the project...'
        // Example: sh 'make build' or npm install
      }
    }

    stage('Unit Test') {
      when {
        expression { env.BRANCH_NAME?.startsWith('feature/') }
      }
      steps {
        echo "Running Unit Tests on ${env.BRANCH_NAME}"
        // Example: sh './run-unit-tests.sh'
      }
    }

    stage('UI Test') {
      when {
        branch 'main'
      }
      steps {
        echo 'Running UI tests...'
        // Example: sh './run-ui-tests.sh'
      }
    }

    stage('Deploy to SIT') {
      when {
        branch 'main'
      }
      steps {
        echo 'Deploying to SIT...'
        // Example: sh './deploy-sit.sh'
      }
    }

    stage('API Test') {
      when {
        branch 'main'
      }
      steps {
        echo 'Running API tests...'
        // Example: sh './run-api-tests.sh'
      }
    }
  }

  post {
    success {
        steps {
            script {
                if (env.BRANCH_NAME == 'main') {
                    echo '✅ Post Action: Full pipeline on main completed successfully.'
                }
            }
        }
    }

    failure {
        steps {
            script {
                if (env.BRANCH_NAME == 'main') {
                    echo '❌ Post Action: Full pipeline on main failed.'
                }
            }
        }
    }
  }

}
