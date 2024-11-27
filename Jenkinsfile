pipeline {
    agent any

    stages {
        stage('Clone repo') {
            steps {
                script {
                    def gitRepoUrl = 'https://github.com/denisterentiev/jenkins-task.git'
                    def yamlFilePath = 'release.yaml'

                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: "${gitRepoUrl}"]])

                    // Ensure the YAML file exists in the workspace
                    if (!fileExists(yamlFilePath)) {
                        error("YAML file not found at ${yamlFilePath}")
                    }
                }
            }
        }
        stage('Read YAML File') {
            steps {
                script {
                    // Path to the YAML file
                    release = readYaml file: 'release.yaml'
                    commitValue = release.application.commit
                    echo "release file contents: ${release}"
                    echo "Application params: ${release.application}"
                    echo "commit: ${release.application.commit}"
                    echo "version: ${release.application.version}"
                    echo "name: ${release.application.name}"
                    echo 'Printing value only.'
                    println(commitValue)
                }
            }
        }
    }
}
