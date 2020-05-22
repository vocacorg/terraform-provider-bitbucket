pipeline{
    agent any
    tools {
        go 'go-1.14.3'
    }
    environment {
        GO111MODULE = 'on'
    }
    stages{
        stage("Clone"){
            steps{
                echo "Cloning the git repository" + env.BRANCH_NAME
                git branch: 'master', url: 'https://github.com/vocacorg/terraform-provider-bitbucket.git'
                echo "Content in working directory"
                sh "ls -la ."
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage("Run Terraform"){
            steps{
                script {
                    def tfHome = tool name: 'Terraform'
                    env.PATH = "${tfHome}:${env.PATH}"
                }
                
                echo "Running terraform files"
                sh 'terraform --version'
                echo "Initialised terraform"
                
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}