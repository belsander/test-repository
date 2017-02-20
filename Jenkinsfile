node {
  stage('Clone repositories') {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: true, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '3ce336a8-46e0-44cd-b594-63892e32a1d6', url: 'ssh://airscm:7999/sm/cb.dev.c']]])
    echo 'Cloning repository...'
  }
  stage('Check repositories') {
    sh "ls -al"
    sh "git submodule update --init --recursive"
  }
}
