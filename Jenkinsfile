pipeline { 
    agent any

    environemnt{
        LOGIN = credentials('login')
    }
                env.LOGIN
                env.LOGIN_USR
                env.LOGIN_PSW
    
    parameters{
        choice(name: 'ENVIRONMENT',
               choices: ['DEVELOPMENT','STAGING', 'PRODUCTION'] ,
               description: 'Choose the environment for this deployment')
        password(name: 'APIKEY',
                 defaultValue: '123ABC',
                 description: 'Passes a secret value into the pipeline')
        text(name:'CHANGELOG' ,
             defaultValue: ' This is the change log' ,
             description: ' Freeform  text can be added to a report ')
                 
    }

    stages { 
        stage('Username-Password')
        {
            Steps{
                withCredentials([string(credentialsId:'apikey', variable: 'APIKEY']){
                    sh " ./build_script.sh${env.APIKEY}"
                }
                            
            }
            
        }
        
        stage('Test'){
            steps{
                echo " Tests the ${params.ENVIRONMENT} environment "
                echo " Can I Tell you a Secret ${params.APIKEY} "
            }
        }
        stage('Deploy') {
            when{
                expression { params.ENVIRONMENT == 'PRODUCTION' }
            }
            steps{
                input message: ' Confirm Deployment to Production ........' , ok: 'Deploy'
                echo " Deploying to ${params.ENVIRONMENT} "
            }
        }
        stage('Report'){
            steps{
                echo " This is a Report Form "
                sh "printf \" Only the Updated One's ${params.CHANGELOG}\" > ${params.ENVIRONMENT}.txt"
                archiveArtifacts allowEmptyArchive: true, 
                    artifacts: '*.txt', 
                    fingerprint: true, 
                    followSymlinks: false, 
                    onlyIfSuccessful: true
                
            }
        }

    }
}    
        
