pipeline {
    agent any
    tools {
        nodejs('NodeJs')
    }
    parameters {
        string(defaultValue: '1.2', description: 'Custom version for the image', name: 'IMAGE_VERSION')
        string(defaultValue: 'name', description: 'name of repo or tag', name: 'IMAGE_NAME')
    }

    stages {
        stage('init') {
            steps {
                script {
                    gv = load 'script.groovy'
                }
            }
        }
        stage('build app') {
            steps {
                script {
                    dir('my-app/') {
                      gv.buildApp()
                    }
                }
            }
        }
        stage('build image') {
            steps {
                script {
                    gv.buildImage(params.IMAGE_VERSION, params.IMAGE_NAME)
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    gv.deployApp(params.IMAGE_VERSION, params.IMAGE_NAME)
                }
            }
        }
    }
}
