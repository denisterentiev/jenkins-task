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
        stage('Read YAML File') {
            steps {
                script {
                    // Path to the YAML file
                    def yamlFile = 'release.yaml'

                    // Read the YAML file
                    def yamlData = readYaml file: yamlFile

                    // Print the contents of the YAML file
                    echo "YAML Data: ${yamlData}"

                    // Example: Access a specific field in the YAML file
                    if (yamlData.someKey) {
                        echo "commit: ${yamlData.someKey}"
                    } else {
                        echo 'someKey not found in the YAML file'
                    }
                }
            }
        }
    }
}

