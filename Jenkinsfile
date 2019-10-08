36 lines (34 sloc)  1.62 KB
  
pipeline {
  agent any
  stages {
    stage('test') {
      steps {
        sh " echo Hello ${params.TEST}"
        sh " echo SSH Host ${params.sshHost}"
      }
    }
    stage('Locust') {
      steps {
        script {
          def remote = [:]
          remote.name = "testrunner"
          remote.host = "${params.sshHost}"
          remote.user = 'testrunner'
          remote.password = "VMware1!"
          remote.allowAnyHosts = true
          script {sshCommand remote: remote, command: "ls -lrt"}
        }

      }
    }
  }
  parameters {
    string(name: 'TEST', defaultValue: 'Jenkins', description: 'Who should I say hello to?')
    string(name: 'sshHost', defaultValue: '100.26.206.96', description: 'SSH Host running Cypress and Locust')
    string(name: 'slackOauthToken', defaultValue: 'abcdefghijklmnopqrstuvwxyz', description: 'Slack Token')
    string(name: 'slackThreadId', defaultValue: 'slackThreadHere', description: 'slackThreadId')
    string(name: 'testSpecPath', defaultValue: '100.26.206.96', description: 'Cypress Test Spec path')
    string(name: 'ipAddress', defaultValue: '100.26.206.96', description: 'Website IP Address')
    string(name: 'websiteBase', defaultValue: '100.26.206.96', description: 'Website Base URI')
  }
}
