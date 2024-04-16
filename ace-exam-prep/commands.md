## set project ID for gcloud CLI
- gcloud config set project $PROJECT_ID

## create repo to store docker images in artifact registry
- gcloud artifacts repositories create hello-repo \
   --repository-format=docker \
   --location=REGION \
   --description="Docker repository"

## get list of available locations
- gcloud artifacts locations list

## build and tag docker image for hello-app
- docker build -t REGION-docker.pkg.dev/${PROJECT_ID}/hello-repo/hello-app:v1 .

## get list of docker images available
- docker images

## add IAM policy bindings to service account
- gcloud artifacts repositories add-iam-policy-binding hello-repo \
    --location=REGION \
    --member=serviceAccount:PROJECT_NUMBER-compute@developer.gserviceaccount.com \
    --role="roles/artifactregistry.reader"

## run image in docker container using local docker engine
- docker run --rm -p 8080:8080 REGION-docker.pkg.dev/${PROJECT_ID}/hello-repo/hello-app:v1

## push docker image to artifact registry
- gcloud auth configure-docker REGION-docker.pkg.dev
- docker push REGION-docker.pkg.dev/${PROJECT_ID}/hello-repo/hello-app:v1

## set compute engine region
- gcloud config set compute/region REGION

## create GKE cluster
-  gcloud container clusters create-auto hello-cluster

## deploy docker image on GKE cluster
- gcloud container clusters get-credentials hello-cluster --region REGION
- kubectl create deployment hello-app --image=REGION-docker.pkg.dev/${PROJECT_ID}/hello-repo/hello-app:v1
- create HorizontalPodAutoscaler resource for deployment;
kubectl autoscale deployment hello-app --cpu-percent=80 --min=1 --max=5



