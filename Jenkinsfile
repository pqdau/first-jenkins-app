node {
   def commit_id
   stage('Preparation') {
     checkout scm
     sh "git rev-parse --short HEAD > .git/commit-id"                        
     commit_id = readFile('.git/commit-id').trim()
   }
   stage(‘compile') {
       nodejs(nodeJSInstallationName: 'NodeJs') {
       sh 'npm install’
       }
   }
   stage('docker build/push') {
     docker.withRegistry('https://index.docker.io/v1/’, 'dockerhub') {
       def app = docker.build("pqdau/nodejs-demo-with-docker:${commit_id}", '.').push()
     }
   }
}
