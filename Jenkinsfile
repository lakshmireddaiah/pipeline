pipeline {
    agent any
     environment {
            DOCKERIMAGENAME = 'node-rest-api:v2.0.0'   //MONGODB = false
    }

    stages {
        stage('Prepare') {
            steps{//deleteDir();
                sh ' echo present working directory is ';sh 'pwd';}
        }  
        stage('BuildDockerImage') {
            steps{
                sh 'sudo docker build -t cpsbatthoutlook/${DOCKERIMAGENAME} .'                
                //sh 'sudo docker inspect cpsbatthoutlook/${DOCKERIMAGENAME}'
            }
        }   
        stage('StartMongoDb') {
            steps
            {
                 sh 'sudo docker start mongodb'
                 sh '/bin/bash runDockerContainer.sh start mongodb'
                // MONGODB = true 
                // script { //MongoDB is running?
                //     if (${MONGODB} == false ) {
                //         sh 'sudo docker start mongodb'; MONGODB = true  }
                //     else {sh 'MondoDB should be already up'}
                // }
            }
        }
        stage('DockerStartNodeJs1') {
            steps {
                sh ' sudo docker run -p 8081:3000 -d cpsbatthoutlook/${DOCKERIMAGENAME}'
            }
        }
        // stage('DockerStartNodeJs2') {
        //     agent {
        //         docker { 
        //             image 'cpsbatthoutlook/${DOCKERIMAGENAME}'
        //             reuseNode true
        //             args '-p 8082:3000'
        //         }
        //     }
        //     steps{
        //         echo "sh test the server to be running fine "
        //         sh ' sleep 120'
                
        //     }
        // }
        stage('StopContainersRunning') {
            steps {
                sh '/bin/bash runDockerContainer.sh stop cpsbatthoutlook/${DOCKERIMAGENAME}'
                sh '/bin/bash runDockerContainer.sh stop mongodb'
            }
        }
    }    
}

