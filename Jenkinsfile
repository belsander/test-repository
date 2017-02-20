node {
  stage('Clone repositories') {
    steps {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: true, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'ssh://airscm:7999/sm/cb.dev.c']]])
      echo 'Cloning repository...'
      sh "ls -al"
      sh "git submodule update --init --recursive"
  }
}
