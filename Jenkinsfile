pipeline{
  agent any
  stages{
    stage("Workspace_cleanup"){
    //Cleaning WorkSpace
       steps{
           step([$class: 'WsCleanup'])
       }
    }
    stage('Repo Clone'){
       steps{
           checkout([$class: 'GitSCM', branches: [[name: '*/main']],
           extensions: [], userRemoteConfigs: [[url: 'https://github.com/shubh9975/calsoft.git']]])
       }
    }
    stage('Installing k3s'){
       steps{
          sh '''     
              sudo ansible-playbook k3s/tests/test.yml --tags $k3-setup
          '''
       }
    }

}
}
