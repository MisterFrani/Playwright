pipeline {
  agent {
    docker {
      image 'playwright/chromium:playwright-1.56.1'
      args '--user=root --entrypoint=""'
    }
  }

  stages {
    stage('demarrage de configuration projet') {
      steps {
        // Installer git
        sh 'apt-get update && apt-get install -y git'
        // Supprimer le repo (si existe) puis cloner
        sh 'rm -rf repo'
        sh 'git clone https://github.com/MisterFrani/Playwright.git repo'
      }
    }

    stage('Install package and run test E2E') {
      steps {
        dir('repo') {
          sh 'node -v'
          sh 'npm -v'
          sh 'npx playwright --version'
          sh 'npm ci || npm install'
          sh 'npx playwright test --project=chromium'
        }
      }
    }
  }
}
