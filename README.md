## Create an ACR

Use the command line

- Az Cli 

> az acr create --resource-group PreciousRG --name precioushelmacr --sku Basic 

## Create AKS and Connect to your ACR

 - Az Cli 

 > az aks create --resource-group PreciousRG --name preciousAKS --location eastus --attach-acr precioushelmacr --generate -ssh-keys

- az aks install cli 

> az aks get-credentials --resource-group PreciousRG --name PreciousAKS

 - Using a sample application [VoteAPP](https://github.com/PreciousEddy/azure-voting-app-redis.git)

 - Build and push the sample application to the ACR:
 
  > az acr build --image azure-vote-front:v1 --registry precioushelmacr --file Dockerfile .

 ## Create an Helm Chart.
 - using: 
  > helm create azure-vote-front
 - update azure-vote-front/Chart.yaml to add a dependency for the redis chart from the https://charts.bitnami.com/bitnami chart repository and update appversion to v1.

 - Update your helm chart dependencies using helm dependency update:
 > helm dependency update azure-vote-front

 ## Update _azure-vote-front/values.yaml_:
  - Add a _redis_ section to set the image details, container port, and deployment name.
  - add a _backendName_ for connecting the frontend portion to the _redis_ deployment
  - Change _image.repository_ to <loginServer>/azure-vote-front.
  - change _image.tag_ to v1
  - Change _service.type_ to _Loadbalancer_


## Run the Helm Chart using:
> helm install azure-vote-front azure-vote-front/