 @Library('SnykShared@master')                                                                                                                                                                    
import com.symphony.security.containers.Control
import com.symphony.security.containers.Artifactory


node {
    def gitrepo = 'https://github.com/sandro-lex-symphony/docker-images.git'
    def image_name = 'expbase:1'
    def artifactory_repository = "slex-reg-test/expbase:1"

    stage('Git pull') {
        echo '### Performing git pull for ' + gitrepo
        sh 'pwd'
        git  url: gitrepo
    }

    stage('Docker build') {
        echo '### Going to docker build'
        sh 'docker --version'
        sh 'DOCKER_BUILDKIT=1 docker build -f base1/Dockerfile -t ' +image_name+' base1'
        //sh 'docker build -f bad-examples/Dockerfile-tcpdump -t badimage bad-examples'
    }

    stage('Security Checks') {
        def security = new Control(this)
        security.run(image_name)
    }

    stage('Artifactory') {
        def artifactory = new Artifactory(this)
        artifactory.push(image_name, artifactory_repository)
    }

}
