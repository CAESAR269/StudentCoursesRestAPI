pipeline {
    agent { label 'Docker' }
    triggers { 
        pollSCM('* * * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/khajadevopsmarch23/StudentCoursesRestAPI',
                    branch: 'master'
            }
        }
        stage('build') {
            steps {
                sh 'docker build -t 349431158401.dkr.ecr.ap-south-1.amazonaws.com/scr:latest .'
            }
        }
        stage('scan and push') {
            steps {
                sh 'docker push 349431158401.dkr.ecr.ap-south-1.amazonaws.com/scr:latest'
            }
        }
    }
}
