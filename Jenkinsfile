pipeline{
    agent  any

    stages{
        stage('Clone Repo'){
            steps{
                git branch : 'main' , url :'https://github.com/ShijithDG/shijith-check-git-jenkins.git'
            }
        }
        stage('run python'){
            steps{
                sh 'python3 add.py'
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