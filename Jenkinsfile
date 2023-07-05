pipeline {
    
    agent any

    environment {
        NEXUS_CREDENTIALS = credentials('nexus')
    }

    stages {

        stage("package") {

            steps {
                sh 'rm -fr dist/'
                sh 'python3 -m build'
            }

        }

        stage("test") {

            steps {
                echo 'Here i\'m testing'
            }
        }

        stage("deploy") {

            steps {

                echo 'Deploying application ...'

                sh "python3 -m twine upload --repository-url http://172.17.0.4:8081/repository/usine-dap/ -u ${env.NEXUS_CREDENTIALS_USR} -p ${env.NEXUS_CREDENTIALS_PSW}  dist/*"
                sh "python3 -m twine upload  -u ${env.PYPI_CREDENTIALS_USR} -p ${env.PYPI_CREDENTIALS_PSW}  dist/*"

            }

        }
    }
}