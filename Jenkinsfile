pipeline{
    //installer l'environnement 
    //nodesjs, playwright
    agent{
         docker {
            image 'playwright/chromium:playwright-1.56.1'
            args '--user=root --entrypoint=""'
        } 
    }
    stages{
        stage("démarrage de configuration projet"){
            steps{
                //supprimer le fichier repo
                sh 'rm -rf repo'
            }
        }
        stage("préparation de l'environnement"){
            steps{
                // installer git (nécessaire pour le clone)
                sh 'apt-get update && apt-get install -y git'
            }
        }
        stage("clone du projet"){
            steps{
                //cloner l'adresse git du projet 
                sh "git clone https://github.com/MisterFrani/Playwright.git repo"
            }
        }
        stage(" verification des versions "){
            steps{
                //check version de node et playwright
                sh "node --version"
                sh "npx playwright --version"
            }
        }
        stage("test "){
            steps{
                //acceder au projet repo avec la commannde dir 
                dir('repo'){
                    sh "npm install"
                    sh "npx playwright test --project=chromium"
                }
            }
        }
    }
}