node {
  def project = 'virajtest-167408'
  def appName = 'bookshelf'  
  def imageTag = "gcr.io/${project}/${appName}"
  

  checkout scm

  stage 'Build image'
  sh("docker build -t ${imageTag} .")

  stage 'Push image to registry'
  sh("gcloud docker push ${imageTag}")
  
  stage 'Deploy Application'

  sh("kubectl apply -f deployment/")
}
