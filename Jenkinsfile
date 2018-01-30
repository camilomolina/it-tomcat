#!groovy

node {
    stage('Environment') {
        echo 'Environment'

        checkout scm
    }

    stage('Provisioning') {
        echo 'Provisioning'

        //ansiblePlaybook(credentialsId: 'private_key', inventory: 'inventories/a/hosts', playbook: 'my_playbook.yml')
		ansiblePlaybook(playbook: 'main.yml')
    }
    stage('Results') {
        archive "build/${app}"

        def mailRecipients = "camilo@bennu.cl"
        def jobName = currentBuild.fullDisplayName

        emailext body: '''${SCRIPT, template="groovy-html.template"}''',
            mimeType: 'text/html',
            subject: "[Jenkins] ${jobName}",
            to: "${mailRecipients}",
            replyTo: "${mailRecipients}",
            recipientProviders: [[$class: 'CulpritsRecipientProvider']]
    }
}


