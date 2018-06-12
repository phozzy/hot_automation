pipeline {
    agent any 
    parameters {
        string(name: 'IPA_SERVER', defaultValue: 'dc00.example.lcl', description: 'IPA controller to execute task')
        string(name: 'SERVER_NAME', defaultValue: 'test.example.lcl', description: 'Name of server to deploy')
        string(name: 'FLAVOR', defaultValue: 'Basic-1-4-50', description: 'VM flavor')
        string(name: 'IMAGE_NAME', defaultValue: 'Centos-7-1805', description: 'Name of a source image to deploy server')
        string(name: 'ROOT_SIZE', defaultValue: "50", description: 'size of root partition')
        string(name: 'DATA_SIZE', defaultValue: "50", description: 'size for partition to store data')
        string(name: 'SSH_KEY', defaultValue: 'heat_key', description: 'name of ssh key-pair to be used for default user')
        string(name: 'NETWORK', defaultValue: 'my-net1', description: 'id of network to connect server')
        string(name: 'SUBNET', defaultValue: 'my-subnet1', description: 'id of subnet to connect server')
        string(name: 'DESCRIPTION', defaultValue: 'test server', description: 'server description in IPA domain')
    }
    stages {
        stage('CreateServer') {
            steps {
                wrap([$class: 'BuildUser']) {
                    ansiColor('xterm') {
                        ansiblePlaybook(
                        playbook: 'addhost.yml',
                        vaultCredentialsId: "${BUILD_USER_ID}VaultCredentials",
                        installation: 'ansible25',
                        extraVars: [
                            ipa_server: "${params.IPA_SERVER}",
                            cred_name: "${BUILD_USER_ID}",
                            server_name: "${params.SERVER_NAME}",
                            flavor: "${params.FLAVOR}",
                            image_name: "${params.IMAGE_NAME}",
                            root_size: "${params.ROOT_SIZE}",
                            data_size: "${params.DATA_SIZE}",
                            ssh_key: "${params.SSH_KEY}",
                            network_id: "${params.NETWORK}",
                            subnet_id: "${params.SUBNET}",
                            server_description: "${params.DESCRIPTION}"
                        ],
                        colorized: true)
                    }
                }
            }
        }
        stage('Stage 2') {
            steps {
                  wrap([$class: 'BuildUser']) {
                  echo "${BUILD_USER}"
                  echo "${BUILD_USER_ID}VaultCredentials"
                  echo "${BUILD_USER_EMAIL}"
                  }
            }
        }
    }
}
