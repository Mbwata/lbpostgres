node {
    stage('Validate') {
        checkout([$class: 'GitSCM', branches: [[name: '**']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Mbwata/lbpostgres.git']]])
        sh '''liquibase tag $BUILD_NUMBER --url=jdbc:postgresql://8d9c3c07700d:5432/postgres
              liquibase status --verbose --url=jdbc:postgresql://8d9c3c07700d:5432/postgres'''
    }
    stage('Update') {
        sh '''liquibase updateSQL --url=jdbc:postgresql://8d9c3c07700d:5432/postgres
              liquibase update --url=jdbc:postgresql://8d9c3c07700d:5432/postgres'''
    }
    stage('Rollback') {
        sh '''liquibase rollbackSQL $BUILD_NUMBER --url=jdbc:postgresql://8d9c3c07700d:5432/postgres
              liquibase rollback $BUILD_NUMBER --url=jdbc:postgresql://8d9c3c07700d:5432/postgres'''
    } 
    stage('Finalize') {
        sh '''liquibase update --url=jdbc:postgresql://8d9c3c07700d:5432/postgres'''
    }          
    stage('Snapshot') {
        sh '''liquibase --outputFile=snapshot_$BUILD_NUMBER.json snapshot --snapshotFormat=json --url=jdbc:postgresql://8d9c3c07700d:5432/postgres
              mv snapshot_$BUILD_NUMBER.json /var/jenkins_home/snapshots/snapshot_$BUILD_NUMBER.json'''
    }    
}
