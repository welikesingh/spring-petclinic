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
                archiveArtifacts artifacts: '**/spring-petclinic-*.jar'
                junit testResults: '**/TEST-*.xml'
            }
        }


        post {
                success {
                    archiveArtifacts artifacts: '**/spring-petclinic-*.jar'
                    junit testResults: '**/TEST-*.xml'
                    mail subject: 'build stage succeded',
                         from: 'bs_devops@yahoo.com',
                         to: 'bs_devops@yahoo.com',
                         body: "Refer to $BUILD_URL for more details"
                }
                failure {
                    mail subject: 'build stage failed',
                         from: 'bs_devops@yahoo.com',
                         to: 'bs_devops@yahoo.com',
                         body: "Refer to $BUILD_URL for more details"
                }
            }
    }
    
}