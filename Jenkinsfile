pipeline{
    agent any
    tools {
        go 'go-1.14.3'
    }
    environment {
        GO111MODULE = 'on'
    }
    stages{
        stage("Clone and Compile"){
            steps{
                echo "Cloning the git repository"
                git branch: 'master', url: 'https://github.com/vocacorg/terraform-provider-bitbucket.git'
                echo "Content in working directory"
                sh "${pwd()}"
                sh "ls -la ${pwd()}"
                echo "Building the repository"
                sh 'go build'
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