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
                sh "docker tag ${GIT_COMMIT} fintlabs.azurecr.io/nginx:1.17.6-${BUILD_NUMBER}"
                withDockerRegistry([credentialsId: 'fintlabs.azurecr.io', url: 'https://fintlabs.azurecr.io']) {
                    sh "docker push fintlabs.azurecr.io/nginx:1.17.6-${BUILD_NUMBER}"
                }
            }
        }
    }
}
