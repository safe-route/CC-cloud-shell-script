```bash
# Compute engine provisioning

gcloud compute instances create-with-container valhalla-jakarta-server --project=safe-route-351803 --zone=asia-northeast1-b --machine-type=e2-medium --network-interface=network-tier=PREMIUM,subnet=default --maintenance-policy=MIGRATE --provisioning-model=STANDARD --service-account=352707269538-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --tags=http-server,https-server --image=projects/cos-cloud/global/images/cos-stable-97-16919-29-36 --boot-disk-size=10GB --boot-disk-type=pd-balanced --boot-disk-device-name=valhalla-jakarta-server --container-image=gcr.io/safe-route-351803/ipcag/valhalla-gisops:3.0.9 --container-restart-policy=always --container-env=tile_urls=https://download.geofabrik.de/asia/indonesia/java-latest.osm.pbf,min_x=106.4758,min_y=-6.4735,max_x=107.1685,max_y=-5.9192,use_tiles_ignore_pbf=True,force_rebuild=False,force_rebuild_elevation=False,build_elevation=True,build_admins=True,build_time_zones=True --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --labels=container-vm=cos-stable-97-16919-29-36

# Allow ingress to port 8002 (where valhalla listens for requests)

gcloud compute --project=safe-route-351803 firewall-rules create allow-valhalla-port --description="allow port 8002 on valhalla instance." --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:8002 --source-ranges=0.0.0.0/0 --enable-logging

# Test server with 2 pin point lat long from boundary set at environment setup

curl http://35.187.197.248:8002/route --data '{"locations":[{"lat":-6.189626,"lon":106.825811},{"lat":-6.148926,"lon":106.727605}],"costing":"auto","directions_options":{"units":"miles"}}' | jq '.'