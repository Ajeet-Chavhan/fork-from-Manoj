pipeline{
    agent any 

    tools {
       jdk 'java-11'
       maven 'maven'
       }
 stages{
        stage('git checkout'){
           steps{
               git branch: 'main', url: 'https://github.com/Ajeet-Chavhan/fork-from-Manoj.git'
           }

         }
stage('compile'){
           steps{
               sh "mvn compile"
            }
       }
       stage('Build'){
          steps{
              sh "mvn clean install" 
          }
      }
      stage('Docker Build and tag'){
         steps{
            sh "docker build -t ajeetchavhan/puneethrajkumar:1 ."
         }
      }

      stage('Docker image scan'){
           steps{
                sh "trivy image --format table -o trivy-image-report.html ajeetchavhan/puneethrajkumar:1"
           }     
      }
      stage('Containerisation'){
        steps{
            sh '''
             docker stop c1
            docker rm c1
             docker run -it -d --name c1 -p 9000:8080 ajeetchavhan/puneethrajkumar:1

            '''
        }
      }
    stage('Login to Docker Hub') {
                   steps {
                        script {
                            withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                                sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                             }
                         }
                     }
         }

 stage('Pushing image to repository'){
            steps{
               sh 'docker push ajeetchavhan/puneethrajkumar:1'
            }
        }
}
}
      



// pipeline {
//     agent any
//     tools{
//         jdk 'java-11'
//         maven 'maven'
//     }
//     stages{
//         stage('git checkout'){
//             steps{
//                 git branch: 'main', url: 'https://github.com/ManojKRISHNAPPA/test-1.git'
//             }
//         }
//         stage('compile'){
//             steps{
//                 sh "mvn compile"
//             }
//         }
//         stage('Build'){
//             steps{
//                 sh "mvn clean install" 
//             }
//         }
//         stage('Build and Tag Docker file'){
//             steps{
//                 sh "docker build -t manojkrishnappa/puneethrajkumar:1 ."
//             }
//         }
//         stage('Docker image scan'){
//             steps{
//                  sh "trivy image --format table -o trivy-image-report.html manojkrishnappa/puneethrajkumar:1"
//             }
//         }

//         stage('Containersation'){
//             steps{
//                 sh '''
//                     docker stop c1
//                     docker rm c1
//                     docker run -it -d --name c1 -p 9001:8080 manojkrishnappa/puneethrajkumar:1
//                 '''
//             }
//         }

//         stage('Login to Docker Hub') {
//                     steps {
//                         script {
//                             withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
//                                 sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
//                             }
//                         }
//                     }
//         }

//         stage('Pushing image to repository'){
//             steps{
//                 sh 'docker push manojkrishnappa/puneethrajkumar:1'
//             }
//         }


//     }
// }
