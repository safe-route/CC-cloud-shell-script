```bash
# Pulling image from hub.docker.com
docker pull ipcagr1d/saferoute-jwt-auth:1.0

# Tagging pulled image prepping for push to gcr container registry
docker tag ipcagr1d/saferoute-jwt-auth:1.0 gcr.io/safe-route-351803/ipcag/safe-route-jwt-auth:1.0

# Push to gcr registry
docker push gcr.io/safe-route-351803/ipcag/safe-route-jwt-auth:1.0

# Deploy to cloud run from image
gcloud run deploy \ 
 --image=gcr.io/safe-route-351803/ipcag/safe-route-jwt-auth:1.0 \ 
 --port=3000 \
 --region=asia-northeast1 \
 --allow-unauthenticated \
 --platform=managed

# Access to url
https://safe-route-jwt-authentication-ck44nnq7hq-an.a.run.app/