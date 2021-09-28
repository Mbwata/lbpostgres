node {
    stage('validate') {
        checkout([$class: 'GitSCM', branches: [[name: '**']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Mbwata/lbpostgres.git']]])
        withCredentials([string(credentialsId: 'pro_key', variable: 'pro_key')]) {
            sh '''ls -l
                liquibase tag $BUILD_NUMBER
                #liquibase status --verbose --liquibaseProLicenseKey=$pro_key
                '''
            }
    }
    stage('update') {
        sh '''liquibase updateSQL
            liquibase update'''
    }
}
