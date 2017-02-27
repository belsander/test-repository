#!groovy
stage('Tests.') {
  parallel rubocop: {
    node {
      echo 'Running Rubocop test.'
      sh([script: 'chef exec rubocop .'])
    }
  },
  foodcritic: {
    node {
      echo 'Running Foodcritic test.'
      sh([script: 'chef exec foodcritic .'])
    }
  },
  kitchentest: {
    node {
      echo 'Running kitchen test.'
      sh([script: 'chef exec kitchen test --log-level=info --concurrency=6 --destroy=always'])
    }
  }
}

stage('Workspace cleanup.') {
  node {
    echo 'Cleaning up workspace directory.'
    step([$class: 'WsCleanup'])
  }
}
