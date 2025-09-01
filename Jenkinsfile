pipeline{
    agent any
    stages{
        stage('github validation'){
          steps{
                 git url: 'https://github.com/kavyasri017/addressbook-cicd-project'
          }
        }
        stage('compiling the code'){
          steps{
                 sh 'mvn compile'
          }
        }
        stage('testing the code'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa of the code'){
            steps{
                sh 'mvn pmd:pmd'
            }
        }
        stage('package'){
            steps{
                sh 'mvn package'
            }
        }
        stage("deploy the project on tomcat"){
            steps{
                sh "sudo mv /var/lib/jenkins/workspace/pipeline/target/addressbook.war /home/ubuntu/apache-tomcat-8.5.100/webapps/"
            }
        }
    }
post {
        success {
            emailext(
                subject: 'SUCCESS: Job \'${JOB_NAME} [${BUILD_NUMBER}]\'',
                body: "Good news!\n\nThe Jenkins job '${JOB_NAME} [${BUILD_NUMBER}]' was successful.\nCheck it here: ${BUILD_URL}",
                to: 'pandakavya984@gmail.com'
            )
        }
        failure {
            emailext(
                subject: 'FAILURE: Job \'${JOB_NAME} [${BUILD_NUMBER}]\'',
                body: "Oops!\n\nThe Jenkins job '${JOB_NAME} [${BUILD_NUMBER}]' has failed.\nCheck it here: ${BUILD_URL}",
                to: 'pandakavya984@gmail.com'
            )
        }
    }
}
