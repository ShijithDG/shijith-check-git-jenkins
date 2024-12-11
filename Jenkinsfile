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
                sh """
                    # Update the package list
                    sudo apt-get update

                    # Install required dependencies
                    sudo apt-get install -y unzip curl

                    # Remove any old AWS CLI versions and installer files
                    rm -rf awscliv2.zip aws/

                    # Download the AWS CLI version 2 installer
                    sudo curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

                    # Unzip the downloaded installer
                    unzip -o awscliv2.zip

                    # Install AWS CLI version 2
                    sudo ./aws/install --update

                    # Verify the installation
                    aws --version

                """
                echo 'succes the installtion of aws cli '
            }
        }
        stage('Artifact Creation'){
            steps{
                echo 'before making the artifact'
                sh 'tar -cvf my_app.tar.gz add.py '
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