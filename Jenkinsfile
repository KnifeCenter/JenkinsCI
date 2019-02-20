def overriddenParams = [
    string(name: 'S3_DEST_BUCKET', defaultValue: 'knifecenter-jenkins', description: 'The AWS S3 bucket to send the build artifacts to.'),

    //-- BEGIN: This section is for automated testing.
    string(name: 'CRYPT_KEY', defaultValue: 'JkeEumwvvQBCDxypLPBozvrpF2rFNhNL', description: 'Name of Crypt Key Credential'),
    string(name: 'TABLE_PREFIX', defaultValue: '', description: 'Table prefix for DB'),
    string(name: 'S3_DB_BUCKET', defaultValue: 'knifecenter-jenkins', description: 'S3 bucket that holds the DB upload'),
    string(name: 'S3_DB_FILE', defaultValue: 'knifecenter-db.gz', description: 'File in S3 bucket containing development DB dump'),
    string(name: 'SKIP_TEST', defaultValue: '1', description: 'Whether or not to skip tests'),
    //-- END
    
    //-- BEING: this section is for Magento-specific values.
    string(name: 'THEME', defaultValue: 'frontend/Forix/knifecenter', description: 'Name of primary project theme'),
    string(name: 'MAGENTO_VERSION', defaultValue: '2.2', description: 'Current version of Magento'),
    string(name: 'PACKAGIST', defaultValue: 'KnifeCenter-Packagist', description: 'Packagist / composer configuration credential name')
    //-- END
]

def mergedParams = paramMerger {
    parameters = overriddenParams
}

properties([parameters(mergedParams), pipelineTriggers([])])

// To deploy to multiple targets, add more lines below.
// This will likely mean that the overriddenParams variable above needs to be updated.
def inputDevDeployTargets = [
    [ sshUser: 'ec2-user', sshHost: 'ec2-52-90-155-69.compute-1.amazonaws.com', sshPort: '22', sshPath: '/home/ec2-user/site', sshKey: 'KnifeCenter-Generic' ]
]
def inputProdDeployTargets = [
    [ sshUser: 'deploy', sshHost: '', sshPort: '22', sshPath: '', sshKey: '' ]
]

// This is what runs the build / deploy pipeline
pipelinePlugin {
    standardized = true
    devDeployTargets = inputDevDeployTargets
    prodDeployTargets = inputProdDeployTargets
}
