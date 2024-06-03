pipeline {
    agent any

    parameters {
        choice(name: 'Language', choices: ['All', 'C', 'Python', 'Bash'], description: 'Choose the language for the pipeline. Default is All.')
    }

    environment {
        LOG_DIR = "${WORKSPACE}/logs"
    }

    stages {
        stage('Initialize') {
            steps {
                script {
                    sh "mkdir -p ${LOG_DIR}"
                }
            }
        }

        stage('Build C') {
            when {
                expression { return params.Language == 'All' || params.Language == 'C' }
            }
            steps {
                script {
                    sh "mkdir -p ${LOG_DIR}" // Ensure log directory exists
                    sh 'gcc -o hello hello.c > ${LOG_DIR}/c_compile.log 2>&1'
                }
            }
        }

        stage('Run C') {
            when {
                expression { return params.Language == 'All' || params.Language == 'C' }
            }
            steps {
                script {
                    sh "mkdir -p ${LOG_DIR}" // Ensure log directory exists
                    sh './hello > ${LOG_DIR}/c_output.log 2>&1'
                }
            }
        }

        stage('Run Python') {
            when {
                expression { return params.Language == 'All' || params.Language == 'Python' }
            }
            steps {
                script {
                    sh "mkdir -p ${LOG_DIR}" // Ensure log directory exists
                    sh 'python3 hello.py > ${LOG_DIR}/python_output.log 2>&1'
                }
            }
        }

        stage('Run Bash') {
            when {
                expression { return params.Language == 'All' || params.Language == 'Bash' }
            }
            steps {
                script {
                    sh "mkdir -p ${LOG_DIR}" // Ensure log directory exists
                    sh 'bash hello.sh > ${LOG_DIR}/bash_output.log 2>&1'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'logs/*.log', allowEmptyArchive: true
            echo 'Logs have been archived.'
        }
    }
}
