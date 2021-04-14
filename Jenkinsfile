 @Library('SnykShared@master')                                                                                                                                                                    
import com.symphony.security.containers.CheckPackages


node {
    def gitrepo = 'https://github.com/sandro-lex-symphony/docker-images.git'
    def image_name = 'expbase:1'
    stage('Git pull') {
        echo '### Performing git pull for ' + gitrepo
        sh 'pwd'
        git  url: gitrepo
    }

    stage('Docker pull') {
        //echo '### Going to test a docker pull'
        //def cp = new CheckPackages(this)
        //cp.t()

        //  withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'sym-aws-dev', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        //     sh "set +x; echo 'Logging into docker repo'; `aws --region us-east-1 ecr get-login --no-include-email`"
        //     sh 'docker pull 189141687483.dkr.ecr.us-east-1.amazonaws.com/slex-reg-test/debian:buster-slim'
        //     sh 'docker run 189141687483.dkr.ecr.us-east-1.amazonaws.com/slex-reg-test/debian:buster-slim cat /etc/os-release'
        //  }


    }


    stage('Docker build') {
        echo '### Going to docker build'
        sh 'docker --version'
        sh 'docker build -f base1/Dockerfile -t ' +image_name+' base1'
        sh 'docker build -f bad-examples/Dockerfile-tcpdump -t badimage bad-examples'
    }

    stage('### Experimental Checkpackages') {
        sh 'ls -al'
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'sym-aws-dev', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh "set +x; echo 'Logging into docker repo'; `aws --region us-east-1 ecr get-login --no-include-email`"
            sh 'ls -al'
            sh 'pwd'
            sh 'ls -al packages/blacklist.txt'
            sh 'ls -al `pwd`/packages/' 
            sh 'docker run --rm -i -v /:/tmp/j badimage ls -al /tmp/j/'
            sh 'docker run --rm -i -v /:/tmp/j badimage ls -al /tmp/j/home'
            sh 'docker run --rm -i -v /:/tmp/j badimage ls -al /tmp/j/opt'
            sh 'docker run --rm -i -v /:/tmp/j badimage ls -al /tmp/j/mnt'
            //sh 'docker run --rm -i -v /:/tmp/j badimage find / -name blacklist.txt'
            sh 'docker pull 189141687483.dkr.ecr.us-east-1.amazonaws.com/slex-reg-test/checkpackages:debug'
            sh 'docker run --rm -v /var/run/docker.sock:/var/run/docker.sock -v /mnt/stateful_partition/home/jenkins/workspace/ImagesFactory/testDocker/packages/blacklist.txt:/tmp/bl.txt 189141687483.dkr.ecr.us-east-1.amazonaws.com/slex-reg-test/checkpackages:debug ' + image_name + ' /tmp/bl.txt'
            sh 'docker run --rm -v /var/run/docker.sock:/var/run/docker.sock -v /mnt/stateful_partition/home/jenkins/workspace/ImagesFactory/testDocker/packages/blacklist.txt:/tmp/blacklist.txt 189141687483.dkr.ecr.us-east-1.amazonaws.com/slex-reg-test/checkpackages:debug badimage /tmp/blacklist.txt'
        }
    }

     stage('### Experimental Dockle') {
          withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'sym-aws-dev', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh "set +x; echo 'Logging into docker repo'; `aws --region us-east-1 ecr get-login --no-include-email`"
            sh 'docker pull 189141687483.dkr.ecr.us-east-1.amazonaws.com/slex-reg-test/dockle:experimental'
            sh 'docker run --rm -i -v /var/run/docker.sock:/var/run/docker.sock 189141687483.dkr.ecr.us-east-1.amazonaws.com/slex-reg-test/dockle:experimental --exit-code 1 ' + image_name
            sh 'docker run --rm -i -v /var/run/docker.sock:/var/run/docker.sock 189141687483.dkr.ecr.us-east-1.amazonaws.com/slex-reg-test/dockle:experimental --exit-code 1 badimage '
        }
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
