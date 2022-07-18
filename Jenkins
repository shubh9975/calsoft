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
              sudo yum update -y
              sudo amazon-linux-extras install ansible2 -y
              ansible --version         
              sudo ansible-playbook k3s/tests/test.yml --tags $params.k3-setup
          '''
       }
    }

}
}
