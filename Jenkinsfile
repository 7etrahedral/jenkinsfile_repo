pipeline {
  agent any

  stages {
    stage('Clone') {
      steps {
        git url: 'https://github.com/7etrahedral/jenkinsfile_repo.git', branch: "${env.BRANCH_NAME}"
      }
    }

    stage('Unit Test') {
        steps {
             echo "Running Unit Tests on ${env.BRANCH_NAME}"
        // Example: sh './run-unit-tests.sh'
        }
    }

    stage('Trigger Build & Deploy to SIT') {
      when {
        branch 'main'
      }
      steps {
        build job: 'build-and-deploy',
              parameters: [
                string(name: 'BRANCH_TO_BUILD', value: 'sit')
              ],
              wait: true
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
        script {
            if (env.BRANCH_NAME == 'main') {
                echo '✅ Post Action: Full pipeline on main completed successfully.'
            } else if (env.BRANCH_NAME == 'feature/abc') {
                echo '✅ Post Action: this is feature/abc.'
            }
        }
    }

    failure {
        script {
            if (env.BRANCH_NAME == 'main') {
                echo '❌ Post Action: Full pipeline on main failed.'
            } else if (env.BRANCH_NAME == 'main') {
                echo '❌ Post Action: this is feature/abc.'
            }
        }
    }
  }

}
