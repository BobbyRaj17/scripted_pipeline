#!/usr/bin/groovy

// load pipeline functions
// Requires pipeline-github-lib plugin to load library from github

@Library('github.com/BobbyRaj17/pipeline_libs@dev')

def pipeline = new io.bravo.Pipeline()

// podTemplate(label: 'master', containers: [
//     containerTemplate(name: 'docker', image: 'docker:1.12.6', command: 'cat', ttyEnabled: true),
// ],
// volumes:[
//     hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
// ]){

  node ('master') {

    def pwd = pwd()
    def chart_dir = "${pwd}/charts/croc-hunter"

    checkout scm

    // read in required jenkins workflow config values
    def inputFile = readFile('Jenkinsfile.json')
    def config = new groovy.json.JsonSlurperClassic().parseText(inputFile)
    println "pipeline config ==> ${config}"

    // continue only if pipeline enabled
    if (!config.pipeline.enabled) {
        println "pipeline disabled"
        return
    }

    // set additional git envvars for image tagging
    // pipeline.gitEnvVars()


    def acct = pipeline.getContainerRepoAcct(config)

    // tag image with version, and branch-commit_id
    // def image_tags_map = pipeline.getContainerTags(config)

    // compile tag list
    // def image_tags_list = pipeline.getMapValues(image_tags_map)


    def testImage = docker.build("test-image")

    testImage.inside {
        sh 'Heloo!!'
    }

    // stage ('publish container') {
    //
    //   container('docker') {
    //
    //     // perform docker login to container registry as the docker-pipeline-plugin doesn't work with the next auth json format
    //     // withCredentials([[$class          : 'UsernamePasswordMultiBinding', credentialsId: config.container_repo.jenkins_creds_id,
    //     //                 usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
    //     //   sh "docker login -u ${env.USERNAME} -p ${env.PASSWORD} ${config.container_repo.host}"
    //     // }
    //
    //     // build and publish container
    //     pipeline.containerBuildPub(
    //         dockerfile: config.container_repo.dockerfile,
    //         host      : config.container_repo.host,
    //         acct      : acct,
    //         repo      : config.container_repo.repo,
    //         tags      : image_tags_list,
    //         auth_id   : config.container_repo.jenkins_creds_id,
    //         image_scanning: config.container_repo.image_scanning
    //     )
    //
    //     // anchore image scanning configuration
    //     // println "Add container image tags to anchore scanning list"
    //
    //     // def tag = image_tags_list.get(0)
    //     // def imageLine = "${config.container_repo.host}/${acct}/${config.container_repo.repo}:${tag}" + ' ' + env.WORKSPACE + '/Dockerfile'
    //     // writeFile file: 'anchore_images', text: imageLine
    //     // anchore name: 'anchore_images', inputQueries: [[query: 'list-packages all'], [query: 'list-files all'], [query: 'cve-scan all'], [query: 'show-pkg-diffs base']]
    //
    //   }
    //
    // }

  }
// }
