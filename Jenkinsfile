pipeline {
  agent any
  tools { 
        maven 'Maven_3_6_3'  
    }
   stages{
    /* stage('CompileandRunSAST') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=smdemo -Dsonar.organization=setth -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=f6fc24f42103facc3402fdd5a39b0ccec8ea0444'
			}
        }  */
           
       stage('SCA by Prisma Cloud') {
            steps {
                withCredentials([string(credentialsId: 'PCC_PASS', variable: 'pass'), string(credentialsId: 'PCC_USER', variable: 'user')])
                 {
                    environment {
                                user = credentials("PCC_USER")
			        pass = credentials("PCC_PASS")
                        } 
                        script { 
                          docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
                          //unstash 'source'
				  
                        
                              sh 'export PRISMA_API_URL="https://api.prismacloud.io"'
				  
			      sh 'cat ${user}'
                              
				  //sh 'checkov --quiet --soft-fail -d . --use-enforcement-rules -o cli --bc-api-key ${user}::${pass} --prisma-api-url "$PRISMA_API_URL" '
                          
                          }
                        }
                    
                }
            }    
        }
   }
}  
