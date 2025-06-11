pipeline {
  agent any

  environment {
    SLACK_WEBHOOK_URL = credentials('slack-webhook') // Define in Jenkins > Credentials
  }

  stages {
    stage('Clone') {
      steps {
        git url: 'https://github.com/7etrahedral/jenkinsfile_repo.git', branch: "${env.BRANCH_NAME}"
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
      when {
        branch 'main'
      }
      steps {
        echo 'Notifying Slack of successful build...'
        sh '''
          curl -X POST -H 'Content-type: application/json' \
            --data '{"text":"✅ Jenkins Pipeline for *main* completed successfully."}' \
            $SLACK_WEBHOOK_URL
        '''
      }
    }

    failure {
      when {
        branch 'main'
      }
      steps {
        echo 'Notifying Slack of failed build...'
        sh '''
          curl -X POST -H 'Content-type: application/json' \
            --data '{"text":"❌ Jenkins Pipeline for *main* failed."}' \
            $SLACK_WEBHOOK_URL
        '''
      }
    }
  }
}
