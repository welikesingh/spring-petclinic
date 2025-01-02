pipeline {
    agent any
    options { 
        timeout(time: 30, unit: 'MINUTES') 
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git') {
            steps {
                git url: 'https://github.com/welikesingh/spring-petclinic.git', 
                    branch: 'main'
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
    
}