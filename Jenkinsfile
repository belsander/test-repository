node {
  stage('Clone repositories') {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: true, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'ssh://airscm:7999/sm/cb.dev.c']]])
    echo 'Cloning repository...'
  }
  stage('Check repositories') {
    sh "ls -al"
    sh "git submodule update --init --recursive"
  }
}
