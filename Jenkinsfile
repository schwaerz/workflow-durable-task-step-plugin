
node {
    checkout([
        $class: 'GitSCM',
        branches: [[name: env.BRANCH_NAME]],
        doGenerateSubmoduleConfigurations: false,
        extensions: [],
        submoduleCfg: [],
        userRemoteConfigs: [[
            // for github the refspec most probably needs adaption
            url: 'https://github.com/orgi/jenkins.git'
        ]]
    ])

    sh 'mvn install'
}
