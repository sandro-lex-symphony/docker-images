node {
    stage('Preparation') {
        echo '### Stage preparation'
        sh 'ls -al'
    }

    stage('Docker build') {
        echo '### Going to docker build'
        sh 'docker --version'
    }

    stage('Vuln Scan') {
        echo '### Going to scan it'
        sh 'npm install snyk'
        sh 'snyk --version'
    }
}
