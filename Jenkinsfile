node {
  stage('Clone repositories') {
    echo 'Cloning repository and tracking submodules by head of branch...'
    sh 'ssh-keyscan -H -t rsa -p 7999 airscm >> ~/.ssh/known_hosts'
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'SubmoduleOption', disableSubmodules: false, parentCredentials: false, recursiveSubmodules: true, reference: '', trackingSubmodules: true]], submoduleCfg: [], userRemoteConfigs: [[url: 'ssh://airscm:7999/sm/cb.dev.c']]])
  }
  stage('Check repositories') {
    sh "ls -al"
    step([$class: 'WsCleanup'])
  }
}
