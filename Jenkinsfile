pipeline{
    //installer l'environnement node js et playwright
    agent {
        docker {
            //recupérer l'image
            image 'playwright/chromium:playwright-1.56.1'
            //donner la permission
            args '--user=root --entrypoint=""'
        }
    }

    satges{
        satge("demarrage de configuration de projet"){
            steps{
                //creer une commande pour suprimer le repo
                sh "rm -rf repo"
            }
            steps{
                //recupération du projet(clone)
                sh "git clone https://github.com/eloundou843-commits/Playwrightjenkins.git repo"
            }
            steps{
                //check version node et playwright
                sh "echo 'node --version'"
                sh "echo 'npx playwright --version'"
            }
            steps{
                //accéder au dossier repo avec la commande dir
                dir('repo'){
                    sh "npm install"
                    sh "npx playwright test --project=chromium"
                }
            }
        }
    }
}