pipeline {
    agent {
        node{
            label 'ROBOSHOP'
        }
    }

 environment { 
       def appVersion = ""
       ACC_ID= 102882775001
       PROJECT= "roboshop"
       COMPONENT ="catalogue"
    }

options {
    disableConcurrentBuilds()
        timeout(time: 15, unit: 'MINUTES') 
    }

/* parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    } */

    // Build
    stages {
        stage('Read version'){
            steps{
                script{
                    def jsonContent = readJSON file: 'package.json'
                    
                    // Extract the version field
                   appVersion = jsonContent.version
                    
                    echo "The extracted version is: ${appVersion}"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    sh """
                        npm install
                       
                    """
                    
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                      withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ACC_ID.dkr.ecr.us-east-1.amazonaws.com
                    docker build -t ${ACC_ID}.102882775001.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${appVersion} .
                    docker push ${ACC_ID}.102882775001.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${appVersion}
                }   
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh """
                        echo "Building.."
                    """
                }
            }
        }
    }

     post { 
        always { 
            echo 'I will always say Hello again!'
        }
        success { 
            echo 'I will run when success'
        }
        failure { 
            echo 'I will run when failure'
        }
    }
}