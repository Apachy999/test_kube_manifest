node('master') {
  def version = "jenikins"
  def name = "apachy/test_sas"
  def dockerRegistry = "https://docker.io"
  def registryCredential = "dockerhub"
  def image

  stage ("Checkout") {
    checkout scm
  }

  stage ("Docker: Build") {
      image = docker.build(
              "${name}:${version}",
              "--network=host .",
              //"-f ./Dockerfiles/i2_web.Dockerfile ./Dockerfiles"
      )
  }

  stage ("Docker: Push") {
        docker.withRegistry('', registryCredential) {
          image.push "${version}"
          echo "Docker Image pushed: ${name}:${version}"
        }
  }
}
