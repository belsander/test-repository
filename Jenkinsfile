node {
  stage('Setting SSH know_hosts.') {
    echo 'Preparing SSH client for host key validation.'
    sh 'touch ~/.ssh/known_hosts'
    sh 'ssh-keygen -R \'[airscm]:7999\''
    sh 'ssh-keyscan -t rsa -p 7999 airscm >> ~/.ssh/known_hosts'
  }
  stage('Clone repositories.') {
    echo 'Cloning repository and tracking submodules by head of branch...'
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'SubmoduleOption', disableSubmodules: false, parentCredentials: false, recursiveSubmodules: true, reference: '', trackingSubmodules: true]], submoduleCfg: [], userRemoteConfigs: [[url: 'ssh://airscm:7999/sm/cb.dev.c']]])
  }
  stage('Rubocop') {
    step([$class: 'WarningsPublisher', consoleParsers: [[parserName: 'Rubocop']])
  }
  stage('Workspace cleanup.') {
    echo 'Cleaning up workspace directory...'
    step([$class: 'WsCleanup'])
  }
}
