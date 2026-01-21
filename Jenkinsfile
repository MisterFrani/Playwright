
pipeline {
  agent {
    docker {
      image 'playwright/chromium:playwright-1.56.1'
      args '--user=root --entrypoint=/bin/bash'
    }
  }

  stages {
    stage('demarrage de configuration projet') {
      steps {
        //Supprimer le repo
        sh 'rm -rf repo'
      }
      steps {
        // Git clone  du repo
        sh 'git clone https://github.com/MisterFrani/Playwright.git repo'
      }
    }

    stage('Install package and run test E2E') {
      steps {
        dir('repo') {
          sh 'echo "node -v"'
          sh 'echo "npm -v"'
          sh 'echo "npx playwright --version"'
          sh 'npm install'
          sh 'npx playwright test --project=chromium'
        }
      }
    }
  }

}
