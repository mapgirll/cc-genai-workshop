## Deploy an Azure AKS Cluster

1. Define the environment variables to be used by the resources definition.

   > **NOTE**: In the following section, we'll create some environment variables. If your terminal session restarts, you may need to reset these variables. You can do that using the following command:
   >
   > ```console
   > source ~/workshopvars.env
   > ```

   ```bash
   export RESOURCE_GROUP=tigera-workshop
   export CLUSTERNAME=aks-workshop
   export LOCATION=canadacentral
   # Persist for later sessions in case of disconnection.
   echo export RESOURCE_GROUP=$RESOURCE_GROUP >> ~/workshopvars.env
   echo export CLUSTERNAME=$CLUSTERNAME >> ~/workshopvars.env
   echo export LOCATION=$LOCATION >> ~/workshopvars.env
   ```

2. If not created, create the Resource Group in the desired Region.
   
   ```bash
   az group create \
     --name $RESOURCE_GROUP \
     --location $LOCATION
   ```
   
3. Create the AKS cluster without a network plugin.
   
   ```bash
   az aks create \
     --resource-group $RESOURCE_GROUP \
     --name $CLUSTERNAME \
     --kubernetes-version 1.27 \
     --location $LOCATION \
     --node-count 2 \
     --node-vm-size Standard_B2ms \
     --max-pods 100 \
     --generate-ssh-keys \
     --network-plugin azure
   ```

4. Configure ```kubectl``` to connect to your cluster.
   
   ```az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTERNAME```