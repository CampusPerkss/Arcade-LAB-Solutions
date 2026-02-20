### GSP647 : Configuring IAM Permissions with gcloud

```
gcloud compute ssh centos-clean --zone=$(gcloud compute project-info describe --format="value(commonInstanceMetadata.items[google-compute-default-zone])") --quiet
```
```
curl -O https://raw.githubusercontent.com/CampusPerkss/google-cloud-arcade/refs/heads/main/2026/January%20Solutions/Arcade%20Week%204%20/lab1.sh
sudo chmod +x lab1.sh
./lab1.sh
```

### LAB 2 : Enhance Scalability Using Managed instance Groups
## Only edit region

```
gcloud compute instance-groups managed create dev-instance-group --template=dev-instance-template --size=1 --region=[enter region] && gcloud compute instance-groups managed set-autoscaling dev-instance-group --region=[enter region] --min-num-replicas=1 --max-num-replicas=3 --target-cpu-utilization=0.6 --mode=on
```

### LAB 3 : Deploy VM with Multiple Network Interfaces in Google Cloud
## only edit region from it 

```
gcloud compute instances create multi-nic-vm --zone=europe-west4-c --machine-type=e2-medium --network-interface=network=my-vpc1,subnet=subnet-a --network-interface=network=my-vpc2,subnet=subnet-b
```

### Arcade 2026 Februay Sprint 4 
## 6 MCQ Questions Only 
