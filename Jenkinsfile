#!groovy
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
}

stage('Archive artifacts.') {
  node {
    echo 'Archiving artifacts in Jenkins.'
    archive('Berksfile')
  }
}

stage('Workspace cleanup.') {
  node {
    echo 'Cleaning up workspace directory.'
    step([$class: 'WsCleanup'])
  }
}
