pipeline {
    agent { label 'node' }
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
                sh 'docker image build -t caesar269/src:latest .'
            }
        }
        stage('push') {
            steps {
                sh 'docker image push caesar269/src:latest'
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