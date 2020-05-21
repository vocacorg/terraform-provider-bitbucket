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
                lists = sh(script: "ls -la .", returnStdout: true)
                echo "Building the repository: ${lists}"
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