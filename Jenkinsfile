node {
  def project = 'virajtest-167408'
  def appName = 'bookshelf'  
  def imageTag = "gcr.io/${project}/${appName}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}"
  

  checkout scm

  stage 'Build image'
  sh("docker build -t ${imageTag} .")

  stage 'Push image to registry'
  sh("gcloud docker push ${imageTag}")
  
  stage 'Deploy Application'
  sh("sed -i.bak 's#gcr.io/virajtest-167408/bookshelf#${imageTag}#' bookshelf-worker.yaml")
  sh("sed -i.bak 's#gcr.io/virajtest-167408/bookshelf#${imageTag}#' bookshelf-frontend.yaml")
  sh("kubectl apply -f *.yaml")
}
