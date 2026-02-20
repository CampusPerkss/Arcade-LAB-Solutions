### GSP647 : Configuring IAM Permissions with gcloud

```
gcloud compute ssh centos-clean --zone=$(gcloud compute project-info describe --format="value(commonInstanceMetadata.items[google-compute-default-zone])") --quiet
```
```
curl -O https://raw.githubusercontent.com/CampusPerkss/google-cloud-arcade/refs/heads/main/2026/January%20Solutions/Arcade%20Week%204%20/lab1.sh
sudo chmod +x lab1.sh
./lab1.sh
```
