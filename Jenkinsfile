pipeline {
    agent any

    stages {
        stage("Manage kubernetes cluster"){
            steps {
                script{
                    withAWS(credentials: 'CB-dev-awscredentials', region: 'us-east-1') {
                        if($Environment=="DEVELOPMENT"){
                           
                            sh "aws eks --region us-east-1 update-kubeconfig --name CB_cluster_Dev"
                            sh "kubectl get svc"
                        }
                        //if ("${Environment}"=="QA"){
                        //   sh  "kubectl config use-context arn:aws:eks:ap-southeast-2:365956504116:clustCO"
                        //}
                        //if ("${Environment}"=="PRODUCTION"){
                        //   sh "kubectl config use-context arn:aws:eks:ap-southeast-2:36595650416fJB"
                        //}}
                    }
                }
            }
        }

        stage("Deploying  culturebie-comments-processor Kubernetes") {
            steps {
                script{
                    dir("culturebie-comments-processor"){
                        sh "kubectl apply -f culturebie-comments-processor.yml"
                    }
                }
            }
        }
        stage("Deploying culturebie_csv_downloader to Kubernetes") {
            steps {
                script{
                    dir("culturebie_csv_downloader"){
                        sh " kubectl apply -f culturebie_csv_downloader.yml"
                    }
                }
            }
        }
        stage("Deploying culturebie_upload_processor to Kubernetes") {
            steps {
                script{
                    dir("culturebie_upload_processor"){
                        sh "kubectl apply -f culturebie_upload_processor.yml"
                    }
                }
            }
        }
        stage("Deploying sqspollerandstatustracker to Kubernetes") {
            steps {
                script{
                    dir("sqspollerandstatustracker"){
                        sh " kubectl apply -f sqspollerandstatustracker.yml"
                    }
                }
            }
        }
        stage("Deploying userjobexecuter to Kubernetes") {
            steps {
                script{
                    dir("userjobexecuter"){
                        sh "kubectl apply -f userjobexecuter.yml"
                    }
                }
            }
        }
        
    }
}
