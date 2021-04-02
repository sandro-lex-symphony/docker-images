node {
    stage('Preparation') {
        echo '### Stage preparation'
        sh 'ls -al'
    }
    stage('Git pull') {
        echo '### Performing git pull for ' + gitrepo
        sh 'pwd'
        git  url: gitrepo
    }


    stage('Docker build') {
        echo '### Going to docker build'
        sh 'docker --version'
        sh 'ls -al '
    }

    stage('Vuln Scan') {
        echo '### Going to scan it'
        sh 'npm install snyk'
        sh 'snyk --version'
    }
}
