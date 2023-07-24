pipeline {
    agent { label 'match the label and build' }
    options {
        retry(3)
        timeout(time: 30, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        jdk 'JDK_8'
    }
    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/manitverma1987/gameoflife.git',
                    branch: 'master'
            }
        }
         stage('package') {
            steps {
                sh script: 'mvn clean package'
            }
        }

         stage('report') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: '**/target/gameoflife.war'
            }
        }
        

    }
    post {
        success {
            mail subject: "${JOB_NAME}: has completed with suceess",
                 body: "your project is effective \n Build Url ${BUILD_URL}",
                 to: 'all@qt.com'
        }
        failure {
            mail subject: "${JOB_NAME}: has completed with errors",
                 body: "your project is Deffective \n Build Url ${BUILD_URL}",
                 to: 'all@qt.com'
        }
    }
    
}