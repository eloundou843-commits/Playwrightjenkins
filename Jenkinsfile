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

    // parameters{ choice =("navigateur", choice=["chromium", "webkit", "firefox"]) 
    //         defaultvalure
    // }
    parameters{
        choice(name:'navigateur', choices:['chromium', 'webkit', 'firefox'], defaultValue:'chromium',description:'navigateur choisi')
    }

    stages{

        stage("check version node et playwright"){
             steps{
                //check version node et playwright
                sh 'echo node --version'
                sh 'echo npm --version'
            }
        }
        stage("demarrage de configuration de projet et clone du projet"){
            steps{
                //installation de git
                sh 'apt-get update && apt-get install -y git'
                //creer une commande pour suprimer le repo
                sh "rm -rf repo"
                //recupération du projet(clone)
                sh "git clone https://github.com/eloundou843-commits/Playwrightjenkins.git repo"
            }
        }
        // stage("clone du projet"){
        //     steps{
        //         sh 'apt-get update && apt-get install -y git'
        //         //recupération du projet(clone)
        //         sh "git clone https://github.com/eloundou843-commits/Playwrightjenkins.git repo"
        //     }
        // }
        
        stage("accéder au dossier repo avec la commande dir"){
              steps{
                //accéder au dossier repo avec la commande dir
                dir('repo'){
                    sh "npm install"
                    sh 'npx playwright install'
                    //on peut remplacé les 2 ligne pécédente par sh 'npm ci'(permet de nétoyer et faire l'installation)
                    //sh "npx playwright test --project=chromium "
                    script {
                        if(params.navigateur == "chromium"){
                            sh "npx playwright test --project=chromium"
                        }
                    }
                }
            }
        }

            
    }
}


// pipeline {
//     agent {
//         docker {
//             image 'playwright/chromium:playwright-1.56.1'
//             args '--user=root --entrypoint=""'
//         }
//     }

//     stages {
//         stage('Display versions') {
//             steps {
//                 sh 'node --version'
//                 sh 'npm --version'
//             }
//         }
//         stage(" CLONE DU PROJET"){
//             steps{
//                 sh 'apt-get update && apt-get install -y git'
//                 sh "rm -rf repo"
//                 echo 'version du git'
//                 sh 'git --version'
//                 sh "git clone https://github.com/admanehocine/PlaywrightJenkins.git repo"
//                 sh "ls -la repo"
//                   dir('repo'){
//                     sh "npm install"
//                     sh "npx playwright install"
//                     sh "npx playwright test --project=chromium"
//                 }
//             }
//         }
        
      
//     }
   
// }