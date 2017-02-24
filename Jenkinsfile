#!groovy
stage('Setting SSH know_hosts.') {
  node('master') {
    echo 'Preparing SSH client for host key validation.'
    sh([script: 'touch ~/.ssh/known_hosts'])
    sh([script: 'ssh-keygen -R \'[airscm]:7999\''])
    sh([script: 'ssh-keyscan -t rsa -p 7999 airscm >> ~/.ssh/known_hosts'])
  }
}

stage('Clone repositories.') {
  node {
    echo 'Cloning repository and tracking submodules by head of branch.'
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'SubmoduleOption', disableSubmodules: false, parentCredentials: false, recursiveSubmodules: true, reference: '', trackingSubmodules: true]], submoduleCfg: [], userRemoteConfigs: [[url: 'ssh://git@airscm:7999/sm/cb.dev.c']]])
  }
}

stage('Rubocop test.') {
  node {
    echo 'Running Rubocop test.'
    sh([script: 'chef exec rubocop .'])
  }
}

stage('Foodcritic test.') {
  node {
    echo 'Running Foodcritic test.'
    sh([script: 'chef exec foodcritic .'])
  }
}

stage('Kitchen test.') {
  node {
    echo 'Running kitchen test.'
    sh([script: 'chef exec kitchen test --log-level=info --concurrency=6 --destroy=always'])
  }
  post {
    success {
      echo 'Archiving artifacts in Jenkins.'
      step([$class: 'ArtifactArchive', artifacts: 'Berksfile,metadata.rb', fingerprint: true])
    }
    failure {
      echo 'Test failed, not archiving artifacts.'
  }
}

stage('Workspace cleanup.') {
  node {
    echo 'Cleaning up workspace directory.'
    step([$class: 'WsCleanup'])
  }
}
