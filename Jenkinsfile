node {
    stage('validate') {
        checkout([$class: 'GitSCM', branches: [[name: '**']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Mbwata/lbpostgres.git']]])
        withCredentials([string(credentialsId: 'pro_key', variable: 'pro_key')]) {
            sh '''
                liquibase tag $BUILD_NUMBER
                #liquibase status --verbose --liquibaseProLicenseKey=$pro_key
                '''
            }
    }
    stage('update') {
        sh '''#liquibase updateSQL
            #liquibase update'''
    }
    stage('snapshot') {
        sh '''liquibase --outputFile=snapshot_$BUILD_NUMBER.json snapshot --snapshotFormat=json
            '''
    }    
}
