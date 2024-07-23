pipeline {
    
        agent any
   
    parameters { choice(name: 'ACTION', choices: ['apply', 'delete'], description: 'Select the action to perform') }

    stages {

        
                 
            }
        }
               
        stage('apply ') {
             when { expression { 
                   return params.ACTION == 'apply'
                } }
            steps {
               sh 'kubectl apply -f k8-files/deploy/deploy.yaml '
            }
        }
        stage('delete ') {
            when { expression { 
                   return params.ACTION == 'delete'
                }
                }
            steps {
               sh 'kubectl delete -f k8-files/deploy/deploy.yaml'
            }
        }
        
        
    }
    post{
        always{
            emailext body: '''Hi,

     The jenkins has been failed . please check it.

     Thanks
     Devops Team''', subject: 'testing jenkins pipeline: $JOB_URL', to: 'yugandharpilla@outlook.com'
    }
    }
}
