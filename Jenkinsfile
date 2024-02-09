pipeline{
    agent any
    environment{
        MAX_SIZE = 10
        MIN_SIZE = 1
        
    }
    
        stages{
            stage('Default'){
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
            stage('Report'){
                steps{
                   sh 'echo "This is report" > report.txt' 
                   archiveArtifacts allowEmptyArchive: true, 
                   artifacts: '**/report.txt', 
                   fingerprint: true, 
                   followSymlinks: false,
                   onlyIfSuccessful: true
                    
                }
            }
        }
}
