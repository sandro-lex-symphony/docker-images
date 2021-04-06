node {
    def gitrepo = 'https://github.com/sandro-lex-symphony/docker-images.git'
    def image_name = 'expbase:1'
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
        sh 'docker build -f base1/Dockerfile -t ' +image_name+' base1'
    }

    stage('Vuln Scan') {
        echo '### Going to scan it'
        sh 'cd /tmp && wget https://nodejs.org/dist/v10.21.0/node-v10.21.0-linux-x64.tar.xz && tar -xf node-v10.21.0-linux-x64.tar.xz --directory /usr/local --strip-components 1'
        sh 'node --version'
        sh 'npm install -g snyk'
        sh 'snyk --version'
        withCredentials([string(credentialsId: 'SNYK_API_TOKEN', variable: 'SNYK_TOKEN')]) {
            sh 'snyk auth '+SNYK_TOKEN  
        }
        sh 'snyk container test --severity-threshold=high --policy-path=debian-policy ' +image_name 
    }
}
