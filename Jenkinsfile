pipeline {
  agent any
  parameters {
        string(name: 'TEST', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
  stages {
    stage('test') {
      steps {
        sh 'echo "Hello $params.TEST"'
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
          script {sshCommand remote: remote, command: "ls -lrt"}
}
        }
      }
    }
  }
