pipeline {
    agent {
        label "ansible_docker"
    }

    stages {
        stage('main') {
            steps {
                git 'https://github.com/shagovid/example-playbook'
                sh '''ansible-vault decrypt secret --vault-password-file vault_pass
                mkdir -p ~/.ssh/ && mv ./secret ~/.ssh/id_rsa && chmod 400 ~/.ssh/id_rsa
                echo -e "Host github.com\\n   StrictHostKeyChecking no\\n   UserKnownHostsFile=/dev/null" > ~/.ssh/config
                ansible-galaxy install -r requirements.yml -p roles
                ansible-playbook site.yml -i inventory/prod.yml'''
            }
        }
    }
}