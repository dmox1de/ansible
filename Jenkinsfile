pipeline {
    agent any

    environment {
        ANSIBLE_CONFIG = "${WORKSPACE}/ansible.cfg"
    }

    stages {
        stage('Подготовка окружения') {
            steps {
                echo '=== Установка Docker & Клонирование репозиториев ==='
                // Запускаем плейбук с тегами install и deploy
                ansiblePlaybook(
                    playbook: 'firstPlaybook.yml',
                    inventory: 'inventory/stend1/jenkins_hosts',
                    credentialsId: 'jenkins-ssh-key', 
                    tags: 'install,deploy',
                    colorized: true
                )
            }
        }

        stage('Запуск приложений') {
            steps {
                echo '=== Запуск микросервисов ==='
                // Запускаем плейбук с тегом start
                ansiblePlaybook(
                    playbook: 'firstPlaybook.yml',
                    inventory: 'inventory/stend1/jenkins_hosts',
                    credentialsId: 'jenkins-ssh-key',
                    tags: 'start',
                    colorized: true
                )
            }
        }
    }
}