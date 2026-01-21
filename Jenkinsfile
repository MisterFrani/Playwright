pipeline {
  agent {
    docker {
      image 'mcr.microsoft.com/playwright:v1.56.1-jammy'
    }
  }

  stages {
    stage('demarrage de configuration projet') {
      steps {
        sh 'git clone https://github.com/MisterFrani/Playwright.git'
      }
    }

    stage('Install package and run test E2E') {
      steps {
          sh 'node -v'
          sh 'npm -v'
          sh 'npx playwright --version'
          sh 'npm ci || npm install'
          sh 'npx playwright test --project=chromium'
      }
    }
  }
}
