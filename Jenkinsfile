pipeline {
    
        agent any
   
    parameters { choice(name: 'ACTION', choices: ['apply', 'delete'], description: 'Select the action to perform') }

    stages {

        stage('parameter validation'){
            steps{
                 script{
                    if ( "${params.ACTION}" == '' ) {
                echo "please atleast pass one parameter"
            } else {
                echo "The option selected : ${params.ACTION}"
            }                 
                 }
            }
        }
               
        stage('apply ') {
             when { expression { 
                   return params.ACTION == 'apply'
                } }
            steps {
               sh 'kubectl apply -f deploy/deploy.yaml'
            }
        }
        stage('delete ') {
            when { expression { 
                   return params.ACTION == 'delete'
                }
                }
            steps {
               sh 'kubectl delete -f deploy/deploy.yaml'
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
