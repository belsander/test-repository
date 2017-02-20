node {
  stage('Clone repositories') {
    steps {
      checkout([$class: 'GitSCM', branches [[: '*/master]], doGenerateSubmoduleConfigurations: true, userRemoteConfigs: [[url: 'ssh://airscm:7999/sm/cb.dev.c']]])
      echo 'Cloning repository...'
      sh "ls -al"
      sh "git submodule update --init --recursive"
  }
}
