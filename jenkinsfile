pipeline{
    agent any
    environment{
        staging_server = "15.206.168.12"

    }
    stages{
         stage('Git Checkout'){
           git credentialsId: 'gitHub', url: 'https://github.com/Swapnil20001/wordpress.git '
        }
        stage{"deploy to remote"}{
            steps{
                sh 'scp ${WORKSPACE}/* ubuntu@${15.206.168.12}:/var/www/html/wordpress'
            }  
        } 
        stage{"change nginx configuration file"}{
            steps{
                sh 'rm -rf ubuntu@15.206.168.12:/etc/nginx/sites-enabled/*' 
            }
        }
        stage{"copy nginx configure file from github"}{
            steps{
                sh 'scp ${wordpress} ubuntu@15.206.168.12:/etc/nginx/sites-enabled/*' 
            }
        }
        stage{"restart nginx"}{
            steps{
                sh 'service nginx restart ubuntu@15.206.168.12 ' 
            }
        }
    }

    
}