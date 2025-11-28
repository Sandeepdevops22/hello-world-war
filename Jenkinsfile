pipeline {
 //    agent { label 'java' }
    agent none
 stages {
        stage('Hello world war') {
            parallel {

                stage('Checkout') {
                    agent { label 'java' }
                    steps {
                        sh "rm -rf hello-world-war"
                        sh "git clone https://github.com/Sandeepdevops22/hello-world-war"
                    }
                }

                stage('Build') {
                    agent { label 'java' }
                    steps {
                        sh "mvn clean package"
                    }
                }

                stage('Deploy') {
                    agent { label 'java' }
                    steps {
                    sh "sudo cp /home/slave1/workspace/Helloworldwarpipeline/target/hello-world-war-1.0.0.war /opt/apache-tomcat-10.1.49-src/webapps"

                    }
                }

            }
        }
    }
}
