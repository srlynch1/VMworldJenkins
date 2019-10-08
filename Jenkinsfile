pipeline {
  agent any
  stages {
    stage('Cypress') {
      steps {
        script {
          def remote = [:]
          remote.name = "testrunner"
          remote.host = "100.26.206.96"
          remote.allowAnyHosts = true

          node {
            withCredentials([usernamePassword(credentialsId: 'testrunner', usernameVariable: 'userName', passwordVariable: 'password')]) {
              remote.user = userName
              remote.passsword = password
              stage("SSH Steps Rocks!") {
                writeFile file: 'abc.sh', text: 'ls'
                sshCommand remote: remote, command: 'for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done'
                sshPut remote: remote, from: 'abc.sh', into: '.'
                sshGet remote: remote, from: 'abc.sh', into: 'bac.sh', override: true
                sshScript remote: remote, script: 'abc.sh'
                sshRemove remote: remote, path: 'abc.sh'
              }
            }
          }
        }

      }
    }
    stage('Locust') {
      steps {
        script {
          def remote = [:]
          remote.name = "testrunner"
          remote.host = "100.26.206.96"
          remote.allowAnyHosts = true

          node {
            withCredentials([usernamePassword(credentialsId: 'testrunner', usernameVariable: 'userName', passwordVariable: 'password')]) {
              remote.user = userName
              remote.passsword = password
              stage("SSH Steps Rocks!") {
                writeFile file: 'abc.sh', text: 'ls'
                sshCommand remote: remote, command: 'for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done'
                sshPut remote: remote, from: 'abc.sh', into: '.'
                sshGet remote: remote, from: 'abc.sh', into: 'bac.sh', override: true
                sshScript remote: remote, script: 'abc.sh'
                sshRemove remote: remote, path: 'abc.sh'
              }
            }
          }
        }

      }
    }
  }
}