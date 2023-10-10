pipeline {
    agent any 
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select The Environment')
    }
    options {
        ansiColor('xterm')    // Add's color to the output : Ensure you install AnsiColor Plugin.
    }
    stages {
        stage('Terraform Create Network') {
            steps {
                git branch: 'main', url: 'https://github.com/b55-clouddevops/terraform-vpc.git'
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars  -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                }
            }

        stage('Terraform Create ALB') {
            steps {
                git branch: 'main', url: 'https://github.com/b55-clouddevops/terraform-loadbalancers.git'
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                }
            }

        stage('Terraform Create Databases') {
            steps {
                        git branch: 'main', url: 'https://github.com/b55-clouddevops/terraform-databases.git'
                        sh "terrafile -f env-${ENV}/Terrafile"
                        sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                        sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars"
                        sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -auto-approve"
                    }
                }
      
        stage('Backend') {
            parallel {
                stage('Terraform Create Catalogue') {
                    steps {
                                git branch: 'main', url: 'https://github.com/b55-clouddevops/catalogue.git'
                                sh "cd mutable-infra"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001 -auto-approve"
                            }
                        } 
                stage('Terraform Create User') {
                    steps {
                                git branch: 'main', url: 'https://github.com/b55-clouddevops/user.git'
                                sh "cd mutable-infra"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars  -reconfigure"
                                sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001 -auto-approve"
                            }
                        }
                stage('Terraform Create Cart') {
                    steps {
                                git branch: 'main', url: 'https://github.com/b55-clouddevops/cart.git'
                                sh "cd mutable-infra"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001 -auto-approve"
                            }
                        }
                stage('Terraform Create Shipping') {
                    steps {
                                git branch: 'main', url: 'https://github.com/b55-clouddevops/shipping.git'
                                sh "cd mutable-infra"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001 -auto-approve"
                            }
                        }
                stage('Terraform Create Payment') {
                    steps {
                                git branch: 'main', url: 'https://github.com/b55-clouddevops/payment.git'
                                sh "cd mutable-infra"
                                sh "terrafile -f env-${ENV}/Terrafile"
                                sh "terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure"
                                sh "terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001"
                                sh "terraform apply -var-file=env-${ENV}/${ENV}.tfvars -var APP_VERSION=001 -auto-approve"
                            }
                        }
                    }
                }  
            }    
        }                        
