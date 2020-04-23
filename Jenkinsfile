node{
    stage('SCM checkout'){
       git credentialsId: 'git-creds', url: 'https://gitlab.com/nkoubamarius/simple_api.git'
    }
    stage('download student_age.json'){
        sshPublisher(publishers: [sshPublisherDesc(configName: 'dev1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'cd /opt/students', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//students', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'student_age.json')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
    }
    stage('download project'){
        sshPublisher(publishers: [sshPublisherDesc(configName: 'dev1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'cd /opt/students', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//students', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'student_age.py')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false), sshPublisherDesc(configName: 'dev1', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /opt/students
docker login --username "nkoubamarius" --password "Docker2@11" docker.io
docker build -t student_age .

docker tag student_age registry:5000/root/student_age:v1 
docker push registry:5000/root/student_age:v1
docker rmi student_age  registry:5000/root/student_age:v1

cd /opt/playbooks
ansible-playbook student_age_playbook.yml --user=centos --extra-vars "ansible_sudo_pass=centos"
''', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//students', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'Dockerfile')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
    }
}
