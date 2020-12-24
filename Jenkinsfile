pipeline {
agent {
label 'build-server '
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
  
  stage ('NPM Install')
  {  
  steps
      {
           sh "cd /home/ubuntu/workspace/jenkinsangularjob ; sudo npm install"
      }
  }
  
  stage ('NG Build')
  {
  steps
      {
           sh "cd /home/ubuntu/workspace/jenkinsangularjob ; ng build"
      }
  }
  stage ('copying dist folder to nginx')
  {  
  steps
      { 
        
            sh "cd /home/ubuntu/workspace/jenkinsangularjob ; scp -r dist/  root@172.31.35.56:/var/www/ "
      }
        
  }
  stage ('nginx')
  {
  steps
      {
         node('Nginx') {
      sh "cd /home/ubuntu/workspace/jenkinsangularjob/dist ; sudo apt-get install nginx -y"
      sh "cd /home/ubuntu/workspace/jenkinsangularjob/dist ; systemctl start nginx"
          }     
      }  
  }
  
  
    }  
  
}
