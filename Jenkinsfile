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
                echo "Cloning the git repository"
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
        stage("Code Quality"){
            steps{
                echo "Checking code quality"
                sh "sonar-scanner -h"
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
        stage("Build"){
            steps{
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