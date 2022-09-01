pipeline {
    agent none
    stages {
        stage('Typescript') {
            agent {
                docker {
                    image 'node:17-bullseye'
                }
            }
            stages{
                stage('BuildTypscript') {
                    steps {
                        dir('DotnetTemplate.Web/') {
                            sh 'npm install'
                            sh 'npm run build'
                        }
                    }
                }
                stage('LintOnTypescript') {
                    steps {
                        dir('DotnetTemplate.Web/') {
                            sh 'npm run lint'
                        }
                    }
                }
                stage('TypeScriptsTests') {
                    steps {
                        dir('DotnetTemplate.Web/') {
                            sh 'npm t'
                        }
                    }
                }
            }
        }
       stage('BuildCode') {
            agent {
                docker {
                    image 'mcr.microsoft.com/dotnet/sdk:6.0'
                }
            }
            environment {
                DOTNET_CLI_HOME = '/tmp/dotnet_cli_home'
            }
            stages{
                stage('BuildCode') {
                    steps {
                        dir('DotnetTemplate.Web/') {
                            sh 'dotnet build'
                        }
                    }
                }
                stage('RunCTests') {
                    steps {
                        dir('DotnetTemplate.Web.test/') {
                            sh 'dotnet test'
                        }
                    }
                }
            }
        }
    }
}





