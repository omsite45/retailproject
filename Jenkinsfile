pipeline {
    agent any
    environment {
        LABS = credentials('jupyter_lab_creds')

        }
    stages {
        stage('Build') {
            steps {
                sh 'pip3 install --user pipenv'
                sh '/bitnami/jenkins/home/.local/bin/pipenv --rm || exit 0'
                sh '/bitnami/jenkins/home/.local/bin/pipenv install'
                echo "build completed successful awesome"
                

                echo "build completed successful ## this is comment for built success "
                
                }
            }
        stage('Test') {
            steps {
                sh '/bitnami/jenkins/home/.local/bin/pipenv run pytest'
                }
            }
        stage('Package') {
            steps {
                sh 'zip-r retailproject.zip .'

                }
            }
        stage('Deploy') {

            steps {

                sh 'sshpass-p $LABS_PSW scp-o StrictHostKeyChecking=no-r .$LABS_USR@g02.itversity.com:/home/itv014498/retailproject'
                }
            }
        }
    }
