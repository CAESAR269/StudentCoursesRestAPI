pipeline {
    agent { label 'Docker' }
    triggers { 
        pollSCM('* * * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/CAESAR269/StudentCoursesRestAPI.git',
                    branch: 'sprint_1_release'
            }
        }
        stage('build') {
            steps {
                sh 'docker build -t 349431158401.dkr.ecr.ap-south-1.amazonaws.com/scr:latest .'
            }
        }
        stage('push') {
            steps {
                sh 'docker push 349431158401.dkr.ecr.ap-south-1.amazonaws.com/scr:latest'
           }
        }
        stage('deploy') {
            steps {
                sh 'kubectl apply -f ./K8s/mysql-aws.yml'
                sh 'kubectl apply -f ./K8s/flask-aws.yml'
                sh 'sleep 10s'
                sh 'kubectl get svc'
            }
        }
    }
}
