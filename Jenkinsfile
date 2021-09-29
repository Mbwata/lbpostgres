node {
    stage('validate') {
        checkout([$class: 'GitSCM', branches: [[name: '**']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Mbwata/lbpostgres.git']]])
        withCredentials([string(credentialsId: 'pro_key', variable: 'pro_key')]) {
            sh '''
                liquibase tag $BUILD_NUMBER --url=jdbc:postgresql://dcc000e8bc4b:5432/postgres
                liquibase status --verbose --url=jdbc:postgresql://dcc000e8bc4b:5432/postgres
                '''
            }
    }
    stage('update') {
        sh '''liquibase updateSQL --url=jdbc:postgresql://dcc000e8bc4b:5432/postgres
            liquibase update --url=jdbc:postgresql://dcc000e8bc4b:5432/postgres'''
    }
    stage('Rollback') {
        sh '''liquibase rollbackSQL --url=jdbc:postgresql://dcc000e8bc4b:5432/postgres
            liquibase rollback $BUILD_NUMBER --url=jdbc:postgresql://dcc000e8bc4b:5432/postgres'''
    } 
    stage('Finalize') {
        sh '''liquibase update --url=jdbc:postgresql://dcc000e8bc4b:5432/postgres'''
    }          
    stage('snapshot') {
        sh '''liquibase --outputFile=snapshot_$BUILD_NUMBER.json snapshot --snapshotFormat=json --url=jdbc:postgresql://dcc000e8bc4b:5432/postgres
            mv snapshot_$BUILD_NUMBER.json /var/jenkins_home/snapshots/snapshot_$BUILD_NUMBER.json'''
    }    
}
