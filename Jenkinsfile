@Library('ContainersShared@main')                                                                                                                                                                    
import com.symphony.security.containers.SecurityControl
import com.symphony.security.containers.Dockle
import com.symphony.security.containers.CheckPackages
import com.symphony.security.snyk.Container
import com.symphony.security.containers.Artifactory
import com.symphony.security.containers.Builder
import com.symphony.security.containers.ECR


node {
    def gitrepo = 'https://github.com/sandro-lex-symphony/docker-images.git'
    image_name = 'expbase:1'
    dockerfile = 'base1/Dockerfile'
    artifactory_repo = 'slex-reg-test/' + image_name
    context_path = 'base1/'

    def builder = new Builder(this, false, false)
    def security = new SecurityControl(this)
    def artifactory = new Artifactory(this)
    def ecr = new ECR(this)

    stage('Git pull') {
        echo '### Performing git pull for ' + gitrepo
        sh 'pwd'
        git  url: gitrepo
    }

//     stage('All in one bundle --> build check and push') {
//        builder.buildAndPublish(image_name, dockerfile, context_path, artifactory_repo)
//     }

//     stage('Using Security Controls function') {
//       // create container
//       builder.dockerBuild(image_name, dockerfile, context_path)

//       // security checks
//       security.base_image(image_name, dockerfile)

//       // artifactory
//       artifactory.push(image_name, artifactory_repo)
//     }

    stage('Manual Steps') {
        // docker build
        sh "docker build --no-cache -t ${image_name} -f ${dockerfile} ${context_path}"
        
        // ecr
        ecr.isOK()
        ecr.push(${image_name}, ${image_name})
        echo "XXX DONE XXX"

        // checkpackages
//         cp = new CheckPackages(this)
//         cp.run(image_name)

//         // dockle 
//         dockle = new Dockle(this)
//         dockle.base_image(image_name)

//         // snyk test
//         withCredentials([usernamePassword(credentialsId: 'SNYK_BASEIMAGE_TOKEN', usernameVariable: 'FILLER', passwordVariable: 'SNYK_TOKEN')]) {
//             snyk = new Container(this, SNYK_TOKEN)
//             snyk.test(image_name, dockerfile)
//         }

        // artifactory
        // ... 
    }

}
