node{
  def commit_id
  stage('NewMan test'){
    checkout scm
    sh "git rev-parse --short HEAD > .git/commit-id"
    commit_id = readFile('.git/commit-id').trim()
  }
  stage('test'){
   
      sh 'npm install'
      sh 'npm run api-test-lab'
      sh 'node INTVAL.js -d intval_input.json'
  
  }
  stage('docker build/push'){
    docker.withRegistry('https://registry.hub.docker.com','dockerhub'){
      def app = docker.build("rohsakhare/newmancollection:${commit_id}",'.').push()
    }
  }
}