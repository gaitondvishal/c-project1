# c-project1
pipeline(
agent any
stages{
stage ("get project"){
 stage ("get dependencies & pulish build info"){
    sh "mkdir -p build"
    dir ('build') {
    def b = client.run(command: "install ..")
    server.publishbuildinfo b
}
 stage("build/test project"){
      dir ('build') {
      sh "cmake ../ && cmake --build ."
}
}
}
