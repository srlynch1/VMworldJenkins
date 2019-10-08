pipeline {
  agent any
  stages {
    stage('test') {
      steps {
        sh 'echo "test"'
      }
    }
    stage('Locust') {
      steps {
        script {
          def remote = [:]
          remote.name = 'testrunner'
          remote.host = '100.26.206.96'
          remote.user = 'testrunner'
          remote.password = 'VMware1!'
          remote.allowAnyHosts = true
          sshCommand remote: remote, command: "ls -lrt"
}
        }
      }
    }
  }
