## Create an ACR

Use the command line

'''Az Cli
 az acr create --resource-group PreciousRG --name precioushelmacr --sku Basic'''

## Create AKS and Connect to your ACR

'''Az Cli
az aks create --resource-group PreciousRG --name preciousAKS --location eastus --attach-acr precioushelmacr --generate -ssh-keys'''

'''az aks install cli
az aks get-credentials --resource-group PreciousRG --name PreciousAKS'''

## Create an Helm Chart.
