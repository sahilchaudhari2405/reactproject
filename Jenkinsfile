def gv
pipeline {
    agent any
    tools{
        nodejs "NodeJs"
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
                    gv.buildApp()
                }
            }
        }
        stage('build image') {
            when{
                expression
                {
                    BRANCH_NAME == 'master' ||  BRANCH_NAME == 'development'
                }
            }
            steps {
                script {
                    gv.buildImage(params.IMAGE_VERSION,params.IMAGE_NAME)
                }
            }
        }
        stage('deploy') {
             when{
                expression
                {
                     BRANCH_NAME == 'master' ||  BRANCH_NAME == 'development'
                }
            }
            steps {
                script {
                    gv.deployApp(params.IMAGE_VERSION,params.IMAGE_NAME)
                }
            }
        }
    }
}
