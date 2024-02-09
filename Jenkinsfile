pipeline { 
    agent any

    parameters{
        choice(name: 'ENVIRONMENT',
               choices: ['DEVELOPMENT','STAGING', 'PRODUCTION'] ,
               description: 'Choose the environment for this deployment')
    }

    stages { 
        stage("Build"){
            steps{
                echo ' Build the Enviornment'
            }
        }
        stage('Deploy to Non-production Environments')
        {
            when{
                expression { $params.ENVIRONMENT != 'PRODUCTION' }
            }
            steps{
                echo 'Deploying to ${params.ENVIRONMENT}'
            }
        }
        stage('Deploy to Production Environment'){
            when{
                expression { $params.ENVIRONMENT == 'PRODUCTION' }
            }
            steps{
                input message: ' Confirm Deployment to Production ........' , ok: 'Deploy'
                echo 'Deploying to ${params.ENVIRONMENT} '
            }
        }
        
