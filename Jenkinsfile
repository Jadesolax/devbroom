pipeline{
    agent any
    tools {
        nodejs "node"
    }
    stages{
        stage('test'){
            steps{
                echo "Testing stage"
            }
        }

        stage('production'){
            steps{
                echo "Production stage"
                sh '''
                    sudo ssh -i /var/lib/jenkins/jenkbroom.pem -t -o StrictHostKeyChecking=no ubuntu@ec2-18-133-123-222.eu-west-2.compute.amazonaws.com
                    
                    cd /var/www/
                    sudo rm -rf html
                    sudo mkdir html
                    cd html
                    sudo git init   
                    sudo git remote add origin https://github.com/Jadesolax/devbroom.git
                    sudo git pull origin master
                    sudo npm install
                    sudo pm2 kill
                    sudo PORT=3000 pm2 start ./bin/www
                    '''
            }
        }
    
}
}