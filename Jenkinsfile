podTemplate(label: 'docker-builder', cloud: 'kubernetes', namespace: 'jenkins-helm', containers: [
    containerTemplate(
        name: 'jnlp', // named jnlp so you can override standard image
        image: 'ayethin/jnlp-docker',
        ttyEnabled: true,
        privileged: false,
        alwaysPullImage: false,
        workingDir: '/home/jenkins'
    ),
],
volumes: [
    hostPathVolume(mountPath: '/home/jenkins/workspace/', hostPath: '/home/jenkins/workspace/'), // had to mount for app.inside
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
node('docker-builder') {
    
    stage ('test') {
            def app = docker.image('tag')
            app.pull()
            app.inside {
                sh 'ls -alh'
            }
    }
}