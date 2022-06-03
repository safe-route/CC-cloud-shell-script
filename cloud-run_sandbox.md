```bash
# Pulling image from hub.docker.com
docker pull ipcagr1d/safe-route-sandbox:0.1

# Tagging pulled image prepping for push to gcr container registry
docker tag ipcagr1d/safe-route-sandbox:0.1 gcr.io/safe-route-351803/ipcag/safe-route-sandbox:0.1

# Push to gcr registry
docker push gcr.io/safe-route-351803/ipcag/safe-route-sandbox:0.1

# Deploy to cloud run from image
 gcloud run deploy \ 
 --image=gcr.io/safe-route-351803/ipcag/safe-route-sandbox:0.1 \ 
 --port=5000 \
 --region=asia-northeast1 \
 --allow-unauthenticated \
 --platform=managed

 # Access to url
 https://safe-route-sandbox-ck44nnq7hq-an.a.run.app/