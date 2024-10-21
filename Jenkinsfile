pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Melakukan checkout kode dari repository Git
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Menjalankan npm install di dalam container Node.js
                    docker.image('node:18-alpine').inside {
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    // Hentikan semua container yang berjalan
                    sh 'docker stop $(docker ps -aq) || true'

                    // Hapus semua container
                    sh 'docker rm -f $(docker ps -aq) || true'

                    // Hapus jaringan terkait
                    sh 'docker network prune -f || true'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                // Membangun ulang Docker image aplikasi
                sh 'docker build -t node-app .'
            }
        }

        stage('Deploy') {
            steps {
                // Menjalankan Docker Compose untuk membuat ulang container
                sh 'docker-compose up -d --force-recreate'
            }
        }
    }
}
