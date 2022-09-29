pipeline {
    agent any
    environment {
        AWS_DEFAULT_PROFILE='cb-dev'
    }

    stages {
        stage("Manage kubernetes cluster"){
            steps {
                script{
                    //withAWS(credentials: 'CB-dev-awscredentials', region: 'us-east-1') {
                        //if($Environment=="DEVELOPMENT"){
                            sh "aws s3 ls"
                            sh "aws eks --region us-east-1 update-kubeconfig --name CB_cluster_Dev"

                            sh "kubectl get svc"
                        //}
                        //if ("${Environment}"=="QA"){
                        //   sh  "kubectl config use-context arn:aws:eks:ap-southeast-2:365956504116:clustCO"
                        //}
                        //if ("${Environment}"=="PRODUCTION"){
                        //   sh "kubectl config use-context arn:aws:eks:ap-southeast-2:36595650416fJB"
                        //}}
                    //}
                }
            }
        }

        stage("Deploying  to Kubernetes") {
            steps {
                script{
                    
                        sh "kubectl apply -f culturebie-comments-processor.yml"
                        sh " kubectl apply -f culturebie_csv_downloader.yml"
                        sh "kubectl apply -f culturebie_upload_processor.yml"
                        sh " kubectl apply -f sqspollerandstatustracker.yml"
                        sh "kubectl apply -f userjobexecuter.yml"
                        sh "kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml"
                    
                }
            }
        }
        
    }
}
