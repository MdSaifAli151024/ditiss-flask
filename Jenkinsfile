pipeline {
    agent any
    stages {
        
        stage ("SCM checkout") {
            steps{
            git branch: 'main', url: 'https://github.com/MdSaifAli151024/ditiss-flask.git'
          }
        }
        
        stage ('docker image build') {
            steps {
                sh ' /usr/bin/docker image build -t saiffu/flask-demo .'
            }
        }
        
        stage ("docker login") {
            steps {
                sh 'echo dckr_pat_tGCnMd9ULSghmOhiYB1kdDjdTB8 | /usr/bin/docker login -u saiffu --password-stdin'
            }
        }
        
        stage('docker image push') {
            steps {
                sh ' /usr/bin/docker image push saiffu/flask-demo'
            }
        }
        
        stage('give persmission ') {
            steps {
                input 'DO YOU WANT TO PROCEED'
            }
        }
        
        stage('delete service') {
            steps {
                sh '$(which docker) service rm flask-demo'
            }
        }
        
        stage ('create service') {
            steps {
                sh ' $(which docker) service create --name flask-demo  --replicas 3 -p 5000:5000 saiffu/flask-demo'
            }
        }
    }
}
