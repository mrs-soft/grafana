pipeline {

    agent { label 'vm-slave-dev' }

    stages {
        stage('Build and push image') {
            steps {
                script {
                    docker.withRegistry("${dockerRegistry}", 'docker-registry') {
                        def customImage = docker.build(
                            "registry.plotpad.com/grafana:${BUILD_NUMBER}",
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