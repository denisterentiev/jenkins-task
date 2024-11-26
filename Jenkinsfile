pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    def gitRepoUrl = 'https://github.com/denisterentiev/jenkins-task.git'
                    def yamlFilePath = 'release.yaml'

                    git url: gitRepoUrl

                    // Ensure the YAML file exists in the workspace
                    if (!fileExists(yamlFilePath)) {
                        error("YAML file not found at ${yamlFilePath}")
                    }
                }
            }
        }
    }
}

