node {
    currentBuild.result = "SUCCESS"
    try {
        stage('Checkout'){
            checkout scm
        }
        stage("composer_update") {
            // Run composer update
            sh 'composer update'
        }
        stage("unittest") {
            // Run PHPUnit
            sh 'vendor/bin/phpunit'
        }
        // Create new deployment assets
        switch (env.BRANCH_NAME) {
            case "master":
                stage("deploycode") {
                    sh 'echo deploy master!'
                }
                break
            case "develop":
                stage("deploycode") {
                    sh 'echo deploy develop!'
                    
                }
                break
            default:
                // No deployments for other branches
                break
        }
    }
    catch (err) {
        currentBuild.result = "FAILURE"
            mail body: "project build error is here: ${env.BUILD_URL}" ,
            from: 'louisthaihv@gmail.com',
            replyTo: 'louisthaihv@gmail.com',
            subject: 'project build failed',
            to: 'louisthaihv@gmail.com'
        throw err
    }    
}
