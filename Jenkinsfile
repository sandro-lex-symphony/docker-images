 @Library('SnykShared@master')                                                                                                                                                                    
import com.symphony.security.containers.Control


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

    stage('Security Checks') {
        def security = new Control(this)
        security.run(image_name)

        // def cp = new CheckPackages(this)
        // cp.run(image_name)

        // def dockle = new Dockle(this)
        // dockle.run(image_name)   
    }

    // stage('Vuln Scan') {
    //     withCredentials([string(credentialsId: 'SNYK_API_TOKEN', variable: 'SNYK_TOKEN')]) {
    //          def snyk = new Container(this, SNYK_TOKEN)
    //          snyk.test(image_name) // will fail the job if High Vuln found
    //         //  snyk.test('badimage')
    //     }
    // }
}
