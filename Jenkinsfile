pipeline{
    agent {label "agent-1"}
    parameters{
        string(name: 'version', description: 'Enter version')
        choice(name: 'env', choices: ['dev', 'qa', 'prod'], description: 'Pick environment')
    }
    stages{
    stage("backend-cd"){
       steps{
        script{
            withAWS(credentials: 'aws-creds'){
            sh """
                aws eks update-kubeconfig --region us-east-1 --name expense-dev
                cd helm
                sed -i 's/IMAGE_VERSION/${params.version}/g' values.yaml
                helm upgrade --install backend -n expense -f values.yaml . 
                    
                """
            }  
        }
       }
    }
    }
    

}
