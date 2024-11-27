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
                    println "release file contents: ${release}"
                    println "Application params: ${release.application}"
                    println "commit: ${release.application.commit}"
                    println "version: ${release.application.version}"
                    println "name: ${release.application.name}"
                    println 'Printing value only.'
                    println(commitValue)
                }
            }
        }
        stage('Running job with params from the last job') {
            steps {
                script {
                    build job: 'jenkins_second_param', parameters:[string(name: 'commitValue', value: commitValue)]
                }
            }
        }
    }
}
