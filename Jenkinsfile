pipeline {
  agent any
  stages {
    stage('test') {
      steps {
        sh " echo SSH Host ${params.sshHost}"
      }
    }
    stage('Cypress') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: '05e46b61-cab8-41a8-8bc8-e0c60d6e7ea7', passwordVariable: 'password', usernameVariable: 'userName')]) {
          script {
            def remote = [:]
            remote.name = "testrunner"
            remote.host = "${params.sshHost}"
            remote.user = userName
            remote.password = password
            remote.allowAnyHosts = true
            script {sshCommand remote: remote, command: """export SLACK_USER_TOKEN="${params.slackOauthToken}"
            export SLACK_THREAD="${params.slackThreadId}"
            export PATH=$PATH:/usr/bin/:/usr/local/bin/:/home/testrunner/node_modules/.bin/
            sudo -n -E /home/testrunner/node_modules/.bin/cypress run --spec ${params.testSpecPath} --config video=false --reporter json --env host=http://${params.ipAddress}${params.websiteBase} && echo \$?"""}
          }

        }

      }
    }
    stage('Locust') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: '05e46b61-cab8-41a8-8bc8-e0c60d6e7ea7', passwordVariable: 'password', usernameVariable: 'userName')]) {
          script {
            def remote = [:]
            remote.name = "testrunner"
            remote.host = "${params.sshHost}"
            remote.user = userName
            remote.password = password
            remote.allowAnyHosts = true
            script {sshCommand remote: remote, command: """ export WAVEFRONT_PROXY='${params.restWavefrontProxy}'
            export WEBSITE_ADDRESS="${params.ipAddress}"
            export PATH=$PATH:/usr/bin/:/usr/local/bin/
            sudo -E locust --no-web -c ${params.loadTestUsers} -r ${params.loadHatchRate} -f /usr/local/bin/locust_files/locustWavefront.py -t 3m --only-summary --host http://${params.ipAddress}"""}
          }

        }

      }
    }
  }
  parameters {
    string(name: 'sshHost', defaultValue: '18.233.153.169', description: 'SSH Host running Cypress and Locust')
    string(name: 'slackOauthToken', defaultValue: 'abcdefghijklmnopqrstuvwxyz', description: 'Slack Token')
    string(name: 'slackThreadId', defaultValue: 'slackThreadHere', description: 'slackThreadId')
    string(name: 'testSpecPath', defaultValue: '/home/testrunner/titoactions.spec.js', description: 'Cypress Test Spec path')
    string(name: 'ipAddress', defaultValue: 'Commuter-tito-03426-1337974357.us-east-1.elb.amazonaws.com', description: 'Website IP Address')
    string(name: 'websiteBase', defaultValue: '/Tito/', description: 'Website Base URI')
    string(name: 'restWavefrontProxy', defaultValue: 'Commuter-tito-02439-1370868404.us-east-1.elb.amazonaws.com', description: 'Wavefront Proxy')
    string(name: 'loadTestUsers', defaultValue: '100', description: 'Locust max users per second')
    string(name: 'loadHatchRate', defaultValue: '20', description: 'Locust hatch rate users per second')
  }
}
