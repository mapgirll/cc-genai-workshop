## Deploy a Google GKE Cluster

1. REGION=us-east1
echo export REGION=us-east1 >> ~/.bashrc
LOCATION=us-east1-b
echo export LOCATION=us-east1-b >> ~/.bashrc
CLUSTERNAME=gke-calicocloud-workshop
echo export CLUSTERNAME=gke-calicocloud-workshop >> ~/.bashrc

2. gcloud container clusters create $CLUSTERNAME \
--region $REGION \
--node-locations $LOCATION \
--addons HorizontalPodAutoscaling,HttpLoadBalancing,GcePersistentDiskCsiDriver \
--num-nodes 3 \
--enable-intra-node-visibility \
--machine-type e2-medium --cluster-version 1.28

3. gcloud container clusters get-credentials $CLUSTERNAME --region $REGION 