pipeline{
    agent  any

    stages{
        stage('Clone Repo'){
            steps{
                git branch : 'main' , url :'https://github.com/ShijithDG/shijith-check-git-jenkins.git'
            }
        }
        stage('run Scripts'){
            steps{
                sh 'python3 add.py'
                sh 'sudo apt-get update && sudo apt-get install -y awscli'
                echo 'succes the installtion of aws cli '
            }
        }
        stage('Artifact Creation'){
            steps{
                sh 'tar -cvf my_app.tar.gz addition.py mul.py '
            }
        }
        stage('deploy aws'){
            steps{
                    withCredentials([[
                    $class:'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'jenkins-S3'
                ]]){
                    sh 'aws s3 cp my_app.tar.gz s3://shijith-jenkins --region=ap-south-1'
                    echo 'success fully completer'
                }
            }
        }
    }
    post{
        always{
            echo 'cleaning'
        }
        failure{
            echo 'failed'
        }
        success{
            echo 'successed'
        }
    }
}