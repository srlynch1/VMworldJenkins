pipeline {
  agent any
  stages {
    stage('test') {
      steps {
        sh " echo Hello ${params.TEST}"
        sh " echo SSH Host ${params.sshHost}"
        sh 'whoami'
        sh """export SLACK_USER_TOKEN="${params.slackOauthToken}"
                                export SLACK_THREAD="${params.slackThreadId}"
                                export PATH=$PATH:/usr/bin/:/usr/local/bin/:/home/testrunner/node_modules/.bin/
                                sudo -i -u testrunner -E /home/testrunner/node_modules/.bin/cypress run --spec ${params.testSpecPath} --config video=false --reporter json --env host=http://${params.ipAddress}${params.websiteBase} && echo \$?"""
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