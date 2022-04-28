# Rancher-Secrets
This article outlines how to use Rancher Secrets to access remote Git Repositories e.g Gitlab

Helm Chart Directory Structure
<Helm.Chart.Name>
   |
   |_ values.yaml
      Chart.yaml
      charts	
      templates
         |
         |_ deployment.yaml
            service.yaml
            nginx.yaml
            ....

1. Steps to add secret to Rancher to access remote Gitlab Container Registry Image (Docker Build Image)

Below lines from values.yaml:

image:
  #repository: ubuntu
  repository: registry-git.orro.dev/docker-image-builds/microsoft-sentinel   <--REmote Gitlab Repo Image
  pullPolicy: Always
  # Overrides the image tag whose default is the chart appVersion.
  tag: "latest"
  imagePullSecrets:
  - name: microsoft-sentinel-orro-registry  <--Kubectl secret name (Refer to command below)


Syntax:

kubectl create secret docker-registry <Registry name> --docker-server=<Gitlab Docker Registry server> --docker-username=<Docker Build Project Access Token Name> --docker-password=<Project access token> --docker-email=<emailassociatedwith your gitlab registry>

E.g Command

kubectl create secret docker-registry microsoft-sentinel-orro-registry --docker-server=registry-git.orro.dev --docker-username=Shishir-Rancher --docker-password=wnxWasajNHSsenVgEyEB --docker-email=shishir.adhikari@orro.group      
