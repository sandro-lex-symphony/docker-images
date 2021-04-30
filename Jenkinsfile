@Library('SnykShared@master')                                                                                                                                                                    
import com.symphony.security.containers.SecurityControl
import com.symphony.security.containers.Dockle
import com.symphony.security.containers.CheckPackages
import com.symphony.security.snyk.Container
import com.symphony.security.containers.Artifactory
import com.symphony.security.containers.Builder


node {
    def gitrepo = 'https://github.com/sandro-lex-symphony/docker-images.git'
    image_name = 'expbase:1'
    dockerfile = 'base1/Dockerfile'
    artifactory_repo = 'slex-reg-test/' + image_name
    context_path = 'base1/'

    def builder = new Builder(this, false, false)
    def security = new SecurityControl(this)
    def artifactory = new Artifactory(this)

    stage('Git pull') {
        echo '### Performing git pull for ' + gitrepo
        sh 'pwd'
        git  url: gitrepo
    }

    stage('All in one bundle --> build check and push') {
       builder.buildAndPublish(image_name, dockerfile, context_path, artifactory_repo)
    }

    stage('Using Security Controls function') {
      // create container
      builder.dockerBuild(image_name, dockerfile, context_path)

      // security checks
      security.base_image(image_name, dockerfile)

      // artifactory
      artifactory.push(image_name, artifactory_repo)
    }

    stage('Manual Steps') {
        // docker build
        sh "DOCKER_BUILDKIT=1 DOCKER_CONTENT_TRUST=1 docker build --no-cache -t ${image_name} -f ${dockerfile} ${context}"

        // snyk test
        snyk = new Container(this)
        snyk.test(image_name, dockerfile)

        // checkpackages
        cp = new CheckPackages(this)
        cp.run(image_name)

        // dockle 
        dockle = new Dockle(this)
        dockle.base_image(image_name)
    }

}
