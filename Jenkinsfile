 @Library('SnykShared@master')                                                                                                                                                                    
import com.symphony.security.containers.CheckPackages
import com.symphony.security.containers.Dockle
import com.symphony.security.snyk.Container


node {
    def gitrepo = 'https://github.com/sandro-lex-symphony/docker-images.git'
    def image_name = 'expbase:1'
    stage('Git pull') {
        echo '### Performing git pull for ' + gitrepo
        sh 'pwd'
        git  url: gitrepo
    }


    stage('Docker build') {
        echo '### Going to docker build'
        sh 'docker --version'
        sh 'docker build -f base1/Dockerfile -t ' +image_name+' base1'
        //sh 'docker build -f bad-examples/Dockerfile-tcpdump -t badimage bad-examples'
    }

    stage('Check Packages Using Library') {
        def cp = new CheckPackages(this)
        cp.run(image_name)

        def dockle = new Dockle(this)
        dockle.run(image_name)   
    }

    stage('Vuln Scan') {
        def snyk = new Container(this)
        snyk.test(image_name)
    }
    
    // stage('Vuln Scan') {
    //     echo '### Going to scan it'
    //     sh 'wget https://nodejs.org/dist/v10.21.0/node-v10.21.0-linux-x64.tar.xz && tar -xf node-v10.21.0-linux-x64.tar.xz --directory /usr/local --strip-components 1'
    //     sh 'node --version'
    //     sh 'npm install -g snyk'
    //     sh 'snyk --version'
    //     withCredentials([string(credentialsId: 'SNYK_API_TOKEN', variable: 'SNYK_TOKEN')]) {
    //         sh 'snyk auth '+SNYK_TOKEN  
    //     }
    //     sh 'snyk container test --severity-threshold=high --policy-path=debian-policy ' +image_name 
    // }
}
