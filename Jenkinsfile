pipeline {
  agent any
  parameters {
        string(name: 'TEST', defaultValue: 'Jenkins', description: 'Who should I say hello to?')
        //string(name: 'sshHost', defaultValue: '100.26.206.96', description: 'SSH Host running Cypress and Locust')
  }
  stages {
    stage('test') {
      steps {
        sh ' echo Hello ${params.TEST}'
        //sh ' echo "SSH Host ${params.sshHost}"'
      }
    }
    stage('Locust') {
      steps {
        script {
          def remote = [:]
          remote.name = "testrunner"
          remote.host = "100.26.206.96"
          remote.user = 'testrunner'
          remote.password = "VMware1!"
          remote.allowAnyHosts = true
          script {sshCommand remote: remote, command: "ls -lrt"}
}
        }
      }
    }
  }
