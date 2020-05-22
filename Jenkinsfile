pipeline{
    agent any
    tools {
        go 'go-1.14.3'
        terraform 'Terraform'
    }
    environment {
        GO111MODULE = 'on'
    }
    stages{
        stage("Clone"){
            steps{
                sh 'terraform --version'
                echo "Cloning the git repository: " + env.BRANCH_NAME
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
            environment {
                scannerHome = tool 'SonarqubeScanner'
            }
            steps{
                echo "Checking code quality"
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true, credentialsId: 'webhook-secret'
                }
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
        stage("Code Coverage"){
            steps{
                echo "Checking code quality"
                sh "go test -coverprofile=coverage.out ./..."
                sh "mkdir coverage"
                sh "go tool cover -html=coverage.out -o coverage/index.html"
                publishHTML (target : [allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'coverage',
                    reportFiles: 'index.html',
                    reportName: 'Code Coverage'])
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
        stage("Test Cases") {
            when {
                // Only run test cases when the branch name is 'staging'
                expression { env.BRANCH_NAME == 'staging' }
            }
            steps{
                echo "Running the testcases"
                sh "go test -coverprofile=coverage.out ./..."
                sh "mkdir coverage"
                sh "go tool cover -html=coverage.out -o coverage/index.html"
                publishHTML (target : [allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'coverage',
                    reportFiles: 'index.html',
                    reportName: 'Code Coverage'])
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
                echo "Running terraform files"
                sh 'cd examples && terraform init'
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