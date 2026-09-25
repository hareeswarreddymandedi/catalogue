pipeline {
    agent {
        node{
            label 'ROBOSHOP'
        }
    }

 environment { 
       def appVersion = ""
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
        stage('Build') {
            steps {
                script {
                    sh """
                        echo "Building.."
                       
                    """
                    
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh """
                        echo "Building.."
                    """
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