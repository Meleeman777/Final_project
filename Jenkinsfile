pipeline {
    agent { node { label 'Rebrain' } }
    stages {
        stage('Prepare') {
            steps {
                sh 'sudo rm -rf .infra/ docker/ down.sh up.sh Jenkinsfile .gitignore .git/ /opt/odoo-project'
                sh 'cp -r /home/cicd/workspace/odoo-project /opt'
                sh 'sudo chown -R app:app /opt/odoo-project'
                }
            }
        stage ('Build') {
            steps {
                sh 'source /opt/odoo-project/script.sh'
            }
        }
        stage ('Test') {
            steps {
                sh 'pylint /opt/odoo-project/odoo/__init__.py'
                sh 'pylint /opt/odoo-project/odoo/__main__.py'
            }
        }      
        stage ('Start') {
            steps {
                sh 'sudo systemctl start odoo.service'
            }
        }

        }
    }

