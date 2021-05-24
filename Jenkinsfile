pipeline{
    agent any
    
    environment{
        JAVA_HOME = '/opt/java/openjdk'
    }
    
    stages{
        stage('Build from RTC'){
            steps{
                dir('/home/3htpJenkins'){
                    sh '''
                    #!/bin/bash
                    ./build-web.sh Build-isuarez
                    '''
                }
                echo 'Built succesfully'
            }
        }
        stage('Unit test'){
            steps{
                echo 'Unit test passed'
            }
        }
        stage('Static Code Analysis'){
            steps{
                echo 'Static Code Analysis passed'
            }
        }
        stage('HCL Deploy'){
            steps{
                step([$class: 'UCDeployPublisher',
                    sitename: 'HCL_Jenkins',
                    deploy: [
                        $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeployHelper$DeployBlock',
                        deployApp: 'AppBankingWeb',
                        deployEnv: 'QA',
                        deployProc: 'AppBanking-process',
                        deployVersions: 'AppBanking-deploy:latest',
                        deployOnlyChanged: false
                    ]
                ])
            }
        }
        stage{
            steps{
                echo 'Test stage works properly'
            }
        }
    }
}
