pipeline {
    agent { node { label 'project' } }

    stages {
        stage('ansible') {
          environment {
                 TOOL = tool name: 'Ansible', type: 'org.jenkinsci.plugins.ansible.AnsibleInstallation'
                           }
            steps {
              
             
                sh 'ansible -i inventory/myinventory/hosts -m ping -u root'
                sh "hostname;which ansible"
                //sh 'ansible-playbook -i inventory.ini playbook.yml --syntax-check'
                sh 'ansible-playbook -i inventory/myinventory/hosts  playbooks/converge.yml --syntax-check' 
                 
            }
        }
         stage('approval'){
        steps{ 
          script {
          def userInput = input(id: 'confirm', message: 'Apply ansible?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply ansible', name: 'confirm'] ])
            }
             }
          }
        stage('Test') {
            steps {
                
               //sh "ansible-playbook -i inventory.ini  playbook.yml "
               sh 'ansible-playbook -i ansible-collection-kubernetes/inventory/myinventory/hosts  ansible-collection-kubernetes/playbooks/converge.yml --syntax-check'
            }
        }
        stage('Deploy') {
            steps {
              sh "printenv"
            }
        }
    }
}
