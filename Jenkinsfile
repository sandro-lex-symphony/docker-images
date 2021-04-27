 @Library('SnykShared@master')                                                                                                                                                                    
import com.symphony.security.containers.Control
import com.symphony.security.containers.Artifactory
import com.symphony.security.containers.Builder


node {
    def gitrepo = 'https://github.com/sandro-lex-symphony/docker-images.git'
    def image_name = 'expbase:1'
    def artifactory_repository = "slex-reg-test/expbase:1"

    stage('Git pull') {
        echo '### Performing git pull for ' + gitrepo
        sh 'pwd'
        git  url: gitrepo
    }

    stage('build and push') {
        builder = new Builder(this)
        builder.buildAndPublish(image_name, 'base1/Dockerfile', 'base1')
    }

//    stage('Docker build') {
//        echo '### Going to docker build'
//        sh 'docker --version'
//        sh 'DOCKER_BUILDKIT=1 docker build -f base1/Dockerfile -t ' +image_name+' base1'
//        //sh 'docker build -f bad-examples/Dockerfile-tcpdump -t badimage bad-examples'
//    }
//
//    stage('Security Checks') {
//        def security = new Control(this)
//        security.base_image(image_name)
//    }
//
//    stage('Artifactory') {
//        def artifactory = new Artifactory(this)
//        artifactory.push(image_name, artifactory_repository)
//    }
//
}
