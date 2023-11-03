pipeline {
    agent any 
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select The Environment')
    }
    options {
        ansiColor('xterm')    // Add's color to the output : Ensure you install AnsiColor Plugin.
    }
    stages {


        stage('Destroy-EKS') {
            steps {
                dir('EKS') {  git branch: 'main', url: 'https://github.com/b55-clouddevops/kubernetes.git'

                        sh ''' 
                            cd eks 
                            make destroy
                        ''' 
                     }
                 }
            }

        stage('Terraform Destroy Databases') {
            steps {
                        git branch: 'main', url: 'https://github.com/b55-clouddevops/terraform-databases.git'
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                    }
                }

        stage('Terraform Create Network') {
            steps {
                dir('VPC') { git branch: 'main', url: 'https://github.com/b55-clouddevops/terraform-vpc.git'
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars  -reconfigure"
                        sh "terraform destroy -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                    }
                }
            }
        }    
    }                        
