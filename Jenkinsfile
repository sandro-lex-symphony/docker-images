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


    // stage('Docker build') {
    //     echo '### Going to docker build'
    //     sh 'docker --version'
    //     sh 'DOCKER_BUILDKIT=1 docker build -f base1/Dockerfile -t ' +image_name+' base1'
    //     //sh 'docker build -f bad-examples/Dockerfile-tcpdump -t badimage bad-examples'
    // }

    // stage('Security Checks') {
    //     def security = new Control(this)
    //     security.run(image_name)
    // }

    stage('debug') {
        sh 'docker run --rm -i -v /root:/home/hack alpine:latest ls -al /home/hack/.docker'
    }
    // stage('Check Artifactory creds') {
    //     withCredentials([usernamePassword(credentialsId: 'artifactory_registry_svc_user', passwordVariable: 'pwd', usernameVariable: 'username')]) {
    //         sh "DOCKER_BUILDKIT=1 docker login --username ${username} --password \"${pwd}\" artifact.symphony.com"
    //         sh "DOCKER_BUILDKIT=1 docker tag ${image_name} artifact.symphony.com/slex-reg-test/test1:1"
    //         sh "DOCKER_BUILDKIT=1 docker push artifact.symphony.com/slex-reg-test/test1:1"
    //     }
    // }
}
