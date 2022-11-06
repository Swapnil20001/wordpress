pipeline{
    agent any
    environment{
        staging_server = "15.206.168.12"

    }
    stages{
         stage('Git Checkout'){
             steps{
                 sh 'sudo rm -rf wordpress'
                 sh  'git clone https://github.com/Swapnil20001/wordpress.git '
             }
           
        }
        stage("deploy to remote"){
            steps{
                sh 'scp ${WORKSPACE}/* ubuntu@${staging_server}:/var/www/html/wordpress'
            }  
        } 
        stage("change nginx configuration file"){
            steps{
                sh 'sudo rm -rf ubuntu@${staging_server}:/etc/nginx/sites-enabled/*' 
            }
        }
        stage("copy nginx configure file from github"){
            steps{
                sh 'scp ${wordpress} ubuntu@${staging_server}:/etc/nginx/sites-enabled/*' 
            }
        }
        stage("restart nginx"){
            steps{
                sh 'service nginx restart ubuntu@${staging_server}'
        }
    }

    
}
}
