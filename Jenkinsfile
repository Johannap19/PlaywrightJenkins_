
pipeline{
    //installer l'environnement node js et playwright
    agent {
        docker {
            //recupérer l'image
            image 'mcr.microsoft.com/playwright:v1.57.0-noble'
            // image 'mcr.microsoft.com/playwright:v1.57.0-noble' (pas besoin d'installer le git car cette image contient deja le git )
            //donner la permission
            args '--user=root --entrypoint=""'
        }
    }

    // parameters{ choice =("navigateur", choice=["chromium", "webkit", "firefox"]) 
    //         defaultvalure
    // }
    parameters{
        choice(name:'tags', choices:['smoke', 'regression', 'test'],description:'navigateur choisi')
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
                //sh 'apt-get update && apt-get install -y git'
                //creer une commande pour suprimer le repo
                sh "rm -rf repo"
                //recupération du projet(clone)
                sh "git clone https://github.com/Johannap19/PlaywrightJenkins_.git repo"
                sh "npm ci"
                sh "npx playwright --version"
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
                    sh "npx playwright test --grep @smoke --project=chromium"
                        
                    
                }
            }
        }

            
    }

    // post { 
        
    //     success {
            
    //         script {
    //             if (params.tags == 'smoke') {
    //                 build job : 'job_jenkinsfile2'
    //             }
    //         }
    //     }
    // }
}