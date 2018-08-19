
node {

    stage ('checkout scm') {
        dir ('scm-automatic') {
            checkout scm
        }
    }
    stage ('manual checkout') {
        deleteDir()

        def refspec = "+refs/pull/${env.CHANGE_ID}/head:refs/remotes/origin/PR-${env.CHANGE_ID} +refs/heads/master:refs/remotes/origin/master"
        def url = 'https://github.com/orgi/workflow-durable-task-step-plugin.git'
        
        checkout([
            $class: 'GitSCM',
            doGenerateSubmoduleConfigurations: false,
            extensions: [[$class: 'PreBuildMerge', options: [mergeRemote: "refs/remotes/origin", mergeTarget: "PR-${env.CHANGE_ID}"]]],
            submoduleCfg: [],
            userRemoteConfigs: [[
                // for github the refspec most probably needs adaption
                refspec: refspec,
                // the url you need to adjust as well...
                credentialsId: 'github-orgi',
                url: url
            ]]
        ])
        
    }

    stage ('build') {
        sh 'mvn install'
    }
}
