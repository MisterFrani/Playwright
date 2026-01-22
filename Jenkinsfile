pipeline {
  agent {
    docker {
      image 'mcr.microsoft.com/playwright:v1.57.0-noble'
      args '--user=root --entrypoint=""'
    }
  }

  parameters {
    choice(
      name: 'browser',
      choices: ['chromium', 'firefox', 'webkit'],
      description: 'Selecionner le navigateur'
    )
    choice(
      name: 'testType',
      choices: ['@smoke', '@regression'],
      description: 'Selectionner le type de test à exécuter'
    )
  }

  stages {
    stage('démarrage de configuration projet') {
      steps {
        sh 'rm -rf repo'
      }
    }

    stage('clone du projet') {
      steps {
        sh 'git clone https://github.com/MisterFrani/Playwright.git repo'
        dir('repo') {
          sh 'npm ci'
          sh 'npx playwright install'
        }
      }
    }

    stage('verification des versions') {
      steps {
        sh 'node --version'
        dir('repo') {
          sh 'npx playwright --version'
        }
      }
    }

    stage('tests') {
      steps {
        dir('repo') {
          echo "Running tests on ${params.browser} | type: ${params.testType}"

          sh "npx playwright test --project=${params.browser}"
        }
      }
    }

    stage('generate allure report') {
      steps {
        dir('repo') {
          sh 'npx allure generate allure-results --clean --output allure-report'
          stash name: 'allure-results', includes: 'allure-results/*'
        }
    }
/*
  post {
    success  {
      script {
        if (params.testType == '@smoke') {
          build job: 'job_jenkinsfile_2'
        } else {
            echo "Je run mon test regression"
        }
      }
    }
  }
*/

}
