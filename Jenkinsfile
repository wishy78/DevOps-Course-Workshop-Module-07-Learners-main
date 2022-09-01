pipeline {
    agent none
    stages {
        stage('Typescript') {
            agent {
                docker {
                    image 'node:16-alpine'
                }
            }
            stages{
                stage('BuildTypscript') {
                    steps {
                        dir('DotnetTemplate.Web/') {
                            sh 'npm install'
                            sh 'run build'
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
                    image 'mono:latest'
                }
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





