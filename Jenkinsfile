node {
  stage('Clone repositories') {
    echo 'Cloning repository and tracking submodules by head of branch...'
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'SubmoduleOption', disableSubmodules: false, parentCredentials: false, recursiveSubmodules: true, reference: '', trackingSubmodules: true]], submoduleCfg: [], userRemoteConfigs: [[url: 'ssh://airscm:7999/sm/cb.dev.c']]])
  }
  stage('Check repositories') {
    sh "ls -al"
  }
}
