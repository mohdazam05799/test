pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'make build'
      }
    }
    stage('Test') {
      steps {
        echo 'make test'
      }
    }
  }
  post {
    always {
      script {
        def ghStatus = [:]
        ghStatus['context'] = 'Jenkins Pipeline'
        ghStatus['state'] = currentBuild.currentResult == 'SUCCESS' ? 'success' : 'failure'
        ghStatus['description'] = "Build ${ghStatus['state']}"
        ghStatus['targetUrl'] = "${env.BUILD_URL}"
        githubSetCommitStatus ghStatus
      }
    }
  }
}
