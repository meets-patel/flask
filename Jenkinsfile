pipeline {
    agent any
    
    stages {
        stage ('SCM checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/meets-patel/flask.git'
            }
            
        }
        
        stage ('docker image build') {
            steps {
                sh '/usr/bin/docker image build -t meetpatel2223/pythonimage .'
            }
        }
        
        stage ('Docker Login') {
            steps {
                sh 'echo dckr_pat_BywiI2AmHoGCgefxffyJfSJj1NA | /usr/bin/docker login -u meetpatel2223 --password-stdin'
            }
        }
        
        stage ('docker image Push') {
            steps {
                sh '/usr/bin/docker image push meetpatel2223/pythonimage'
            }
        }
        
        stage ('Get the Confirmation from user') {
            steps {
                input 'Do you want to deploy this'
            }
        }
        
        stage ('remove existing service') {
            steps {
                sh '/usr/bin/docker service rm flask-service'
            }
        }
        
        stage ('create docker service') {
            steps {
                sh '/usr/bin/docker service create --name flask-service --replicas 2 -p 4010:4010 meetpatel2223/pythonimage'
            }
        }
        
    }
}
