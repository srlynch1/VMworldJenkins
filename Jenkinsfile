pipeline {
  agent any
  stages {
    stage('Cypress') {
      steps {
        script {
          def remote = [:]
          remote.name = 'testrunner'
          remote.host = '100.26.206.96'
          remote.user = 'testrunner'
          remote.password = 'VMware1!'
          remote.allowAnyHosts = true
          stage('Remote SSH') {
            sshCommand remote: remote, command: "ls -lrt"
            sshCommand remote: remote, command: "for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done"
          }
        }

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
          stage('Remote SSH') {
            sshCommand remote: remote, command: "ls -lrt"
            sshCommand remote: remote, command: "for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done"
          }
        }

      }
    }
  }
}