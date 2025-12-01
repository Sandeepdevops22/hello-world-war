pipeline {
    // agent { label 'java' }
    agent none
    parameters {
        string(name: 'mcmd1', defaultValue: 'clean', description: 'maven clean command')
        booleanParam(name: 'SAMPLE_BOOLEAN', defaultValue: true, description: 'A boolean parameter')
        choice(name: 'mcmd2', choices: ['package', 'compile', 'install', 'validate'], description: 'Choose one option')
    }
    stages {
        stage ('hello-world-war') {
            parallel {
                stage('Checkout') {
                    agent { label 'java' }
                    steps {
                        withCredentials([
                            usernamePassword(credentialsId: 'e8ff0ebb-76da-4871-aa96-6431d2a85ede',
                                usernameVariable: 'MY_USERNAME',
                                passwordVariable: 'MY_PASSWORD'),
                            sshUserPrivateKey(credentialsId: 'a8c29363-fdb7-4bb3-987a-71b42347549b',
                                keyFileVariable: 'KEY_FILE',
                                usernameVariable: 'SSH_USER')
                        ]) {
                            sh "rm -rf hello-world-war"
                            sh "git clone https://github.com/yashusn/hello-world-war"
                        }
                    }
                }

                stage('Build') {
                    agent { label 'java' }
                    steps {
                        sh "mvn $mcmd1 $mcmd2"
                    }
                }
            }
        }

        stage('Deploy') {
            agent { label 'java' }
            steps {
                sh "sudo cp /home/slave1/workspace/job_hello_word_jenkin/target/hello-world-war-1.0.0.war /opt/apache-tomcat-10.1.49/webapps"
            }
        }
    }
}
