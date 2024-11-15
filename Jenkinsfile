pipeline {
    environment {
        DOCKERHUB_CRED = credentials("ritikgupta0114")
    }
    agent any
    stages {
        stage("Stage 1: Git Clone") {
            steps {
                // sh "git clone https://github.com/shouryap1/Talent-Bridge.git"
                sh "ls"
            }
        }

        stage("Stage 2: Backend Testing") {
            steps {
                sh '''
                cd Talent-Bridge/backend/tests
                npm test
                '''
            }
        }

        stage("Stage 3: Build frontend") {
            steps {
                sh '''
                cd Talent-Bridge/frontend
                npm install
                npm run build
                '''
            }
        }

        stage("Stage 4: Creating Docker Image for frontend") {
            steps {
                sh '''
                cd Talent-Bridge/frontend
                docker build -t ritikgupta0114/frontend:latest .
                '''
            }
        }

        stage("Stage 5: Creating Docker Image for backend") {
            steps {
                sh '''
                cd Talent-Bridge/backend
                docker build -t ritikgupta0114/backend:latest .
                '''
            }
        }

        stage("Stage 6: Push Frontend Docker Image") {
            steps {
                sh '''
                docker login -u ${DOCKERHUB_CRED_USR} -p ${DOCKERHUB_CRED_PSW}
                docker push ritikgupta0114/frontend:latest
                '''
            }
        }

        stage("Stage 7: Push Backend Docker Image") {
            steps {
                sh '''
                docker login -u ${DOCKERHUB_CRED_USR} -p ${DOCKERHUB_CRED_PSW}
                docker push ritikgupta0114/backend:latest
                '''
            }
        }
    }
}
