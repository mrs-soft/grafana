pipeline {

    agent { label 'vm-slave-dev' }

    environment {
        dockerRegistry = "https://registry.plotpad.com"
        dockerImageName = "grafana"
    }
    stages {
        stage('Build and push image') {
            steps {
                script {
                    docker.withRegistry("${dockerRegistry}", 'docker-registry') {
                        def customImage = docker.build(
                            "${dockerImageName}:${BUILD_NUMBER}",
                            "--pull --no-cache"
                        )
                        customImage.push()
                    }
                }
            }
        }
    }

    post {
        always {
            step([$class: 'WsCleanup'])
            cleanWs()
        }
    }
}
