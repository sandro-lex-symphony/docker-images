@Library('SnykShared@master')                                                                                                                                                                    
import com.symphony.security.containers.SecurityControl
import com.symphony.security.containers.Dockle
import com.symphony.security.containers.CheckPackages
import com.symphony.security.snyk.Container
import com.symphony.security.containers.Artifactory
import com.symphony.security.containers.Builder


node {
    def gitrepo = 'https://github.com/sandro-lex-symphony/docker-images.git'

    def builder = new Builder(this, true, true)

    stage('Git pull') {
        echo '### Performing git pull for ' + gitrepo
        sh 'pwd'
        git  url: gitrepo
    }

   stage('build and push') {
       image_name = 'expbase:1'
       dockerfile = 'base1/Dockerfile'
       artifactory_repo = 'slex-reg-test/' + image_name

       builder.dockerBuild(image_name, dockerfile, 'base1/', artifactory_repo)
   }

//   stage('Step by Step') {

//   }
    // stage('Docker build') {
    //     echo '### Going to docker build'
    //     sh 'docker --version'
    //     sh 'DOCKER_BUILDKIT=1 docker build -f base1/Dockerfile -t ' +image_name+' base1'
    //     //sh 'docker build -f bad-examples/Dockerfile-tcpdump -t badimage bad-examples'
    // }

    // stage('Security Checks') {
    //     def security = new Control(this)
    //     security.base_image(image_name)
    // }

    // stage('Artifactory') {
    //     def artifactory = new Artifactory(this)
    //     artifactory.push(image_name, artifactory_repository)
    // }

}
