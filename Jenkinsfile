pipeline{
    agent any

    
            stages{
            
            stage('Append to file'){
                steps{
                   sh ''' 
                    echo "This is Report File " 
                    cat <<EOF>> > report.txt 

                    environment{
        MAX_SIZE = 10
        MIN_SIZE = 1
    }
    parameters{
        string(name: 'MOTHER',
               defaultValue: 'MoM',
               description: "Please Enter Your Mother's Name")
        text(name: 'PHRASE',
             defaultValue: 'Mom is the only beautiful thing in the world. She cares more than anyone in the world ',
             description: ' Enter Your Favorite sentences about your mom')
        booleanParam(name: 'RUN_TESTS',
                     defaultValue: true,
                     description: ' Toggle the Box to False')
        choice(name: 'AWS_REGION',
                choices: ['us-east-1', 'us-east-2', 'us-west-1', 'us-west-2'],
                description: ' Select one region to proceed further')
        password(name: 'PASSWORD',
                 defaultValue: ' Password123',
                 description: ' Enter the password that contains atleast 1 spl chr, 1 number, 1 alpha')
    
    }
    
    
        stages{
            stage('Scale_Default'){
                steps{
                    echo " MAX_SIZE = ${env.MAX_SIZE}"
                    echo " MIN_SIZE = ${env.MIN_SIZE}"
                    
                }
            }
            stage('Scale by 10x'){
                environment{
                    MAX_SIZE = 100
                    MIN_SIZE = 10
                }
                steps{
                     echo " MAX_SIZE = ${env.MAX_SIZE}"
                     echo " MIN_SIZE = ${env.MIN_SIZE}"
                }
            }
            stage('Parameters'){
                steps{
                    echo " My Mother name is ${params.MOTHER} "
                    echo " My Favorite Phrase is ${params.PHRASE}"
                    echo " If u dare to do keep the option ${params.RUN_TESTS}"
                    echo " Select a AWS region u want to deploy to ${params.AWS_REGION}"
                    echo " Enter a Secure Password ${params.PASSWORD}"
                }
            }   

            EOF
                    
                    ''' 
                   archiveArtifacts allowEmptyArchive: true, 
                   artifacts: '**/report.txt', 
                   fingerprint: true, 
                   followSymlinks: false,
                   onlyIfSuccessful: true
                    
                }
            }
        }
}
