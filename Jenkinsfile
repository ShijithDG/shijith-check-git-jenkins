pipeline{
    agent  any

    stages{
        stage('Clone Repo'){
            steps{
                echo 'befor connecting to git'
                git branch : 'main' , url :'https://github.com/ShijithDG/shijith-check-git-jenkins.git'
                echo 'after connecting to git'
            }
        }
        stage('run Scripts'){
            steps{
                echo 'before runnign adn installing aws cli to python '
                sh 'python3 add.py'
                sh '''
                            apt-get update
                            apt-get install -y docker.io unzip curl
                            rm -rf awscliv2.zip aws/
                            curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
                            unzip -o awscliv2.zip
                            ./aws/install

                            aws --version
                        '''
                echo 'succes the installtion of aws cli '
            }
        }
        stage('Artifact Creation'){
            steps{
                echo 'before making the artifact'
                sh 'tar -cvf my_app.tar.gz addition.py mul.py '
                echo 'after making the artifacts'
            }
        }
        stage('deploy aws'){
            steps{
                echo 'before deploy'
                    withCredentials([[
                    $class:'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'jenkins-S3'
                ]]){
                    sh 'aws s3 cp my_app.tar.gz s3://shijith-jenkins --region=ap-south-1'
                    echo 'success fully completer'
                }
                echo 'after deploy'
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