pipeline {
  agent any
    tools{
      maven 'M2_HOME'
          }
   stages {
    stage('Git checkout') {
      steps {
         echo 'This is for cloning the gitrepo'
          checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Devolu-shiva/bankproject.git']])
        
                          }
            }
    stage('Create a Package') {
      steps {
         echo 'This will create a package using maven'
         sh 'mvn package'
                             }
            }
      stage('Publish the HTML Reports') {
      steps {
          publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/bankingapp/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
            }
   
  }

       stage('Create a Docker image from the Package bankingapp.jar file restart docker and jenkins') {
      steps {
       echo 'this step to create a docker image of our running application in our remode docker '
        sh 'docker build -t devshivadevops96/bankingservice:4.0 .'
                    }
            }

        stage('Login to Dockerhub') {
      steps {
       withCredentials([usernamePassword(credentialsId: 'shiva-docker-login', passwordVariable: 'passbank', usernameVariable: 'userbank')]) {
    sh 'docker login -u ${userbank} -p ${passbank}'
}
                                                                    }
                                }

       stage('Push the Docker image') {
      steps {
        sh 'docker push devshivadevops96/bankingservice:4.0'
                                }
            }
  
    

    }
}
