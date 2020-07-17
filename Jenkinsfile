pipeline {
    agent { label 'docker' }
    stages {
        stage('Build') {
            steps {
                sh "docker build --tag ${GIT_COMMIT} -f Dockerfile.glibc ."
            }
        }
        stage('Publish') {
            when { branch 'master' }
            steps {
                sh "docker tag ${GIT_COMMIT} fintlabsacr.azurecr.io/nginx:1.17.6-${BUILD_NUMBER}"
                withDockerRegistry([credentialsId: 'fintlabsacr.azurecr.io', url: 'https://fintlabsacr.azurecr.io']) {
                    sh "docker push fintlabsacr.azurecr.io/nginx:1.17.6-${BUILD_NUMBER}"
                }
            }
        }
    }
}
