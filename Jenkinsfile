pipeline{
    agent{
        label 'agent-1'
    }
    options{
        timeout(time: 45, unit: "MINUTES")
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters{
        string(name: 'appVersion', defaultValue: '1.0.0', description: 'What is the application version?')
    }
    environment{
        def appVersion = '' //variable declaration
    }
    stages{
        stage('print the version'){
            steps{
                script{
                    echo "application version: ${params.appVersion}"
                }
            }
        }
        stage('init'){
            steps{
                sh """
                    cd terraform
                    terraform init 
                """
            }
        }
        stage('plan'){
            steps{
                sh """
                    pwd
                    cd terraform
                    terraform plan -var="app_Version=${params.appVersion}
                """
            }
        }
        // stage('deploy'){
        //     steps{
        //         sh """
        //             cd terraform
        //             terraform apply -auto-approve -var="app_Version=${params.appVersion}
        //         """
        //     }
        // }
    }
    post{
        always{
            echo "this will print always"
            deleteDir()
        }
        success{
            echo "this will print when pipeline is success"
        }
        failure{
            echo "this will print when pipeline is failed"
        }
    }
}