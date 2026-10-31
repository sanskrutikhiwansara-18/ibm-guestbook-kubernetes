# IBM Kubernetes Guestbook Final Project — Starter Files

This is a starter project for the Guestbook Kubernetes lab. It includes the application source and Kubernetes manifests needed to practice building an image, deploying it, scaling it, updating it, and rolling it back.

## Important
- These files do not include IBM Cloud credentials, a registry namespace, or a running Kubernetes cluster.
- Replace `REGISTRY`, `NAMESPACE`, and `IMAGE_NAME` in commands/manifests with values from your IBM Skills Network lab.
- The terminal evidence requested by the assignment must come from actually running the commands in your lab. Do not submit sample or invented terminal output.
- The assignment may use a course-provided Guestbook application with Redis or other components. If your lab provides starter files, use those as the source of truth and adapt these files to match.

## Files
- `Dockerfile` — builds the static web app image.
- `index.html` — default version (v1).
- `deployment.yml` — Kubernetes Deployment and Service.
- `hpa.yml` — HorizontalPodAutoscaler example.
- `index-v2.html` — updated page with “Guestbook – v2”.
- `commands.md` — command checklist for the assignment tasks.

## Run locally with Docker
```bash
docker build -t guestbook:v1 .
docker run --rm -p 8080:8080 guestbook:v1
```
Then open `http://localhost:8080`.

## Build and push to IBM Cloud Container Registry
Log in to IBM Cloud and your container registry using the commands documented by your lab. Then build/tag/push, replacing placeholders:
```bash
ibmcloud cr images
docker build -t guestbook:v1 .
docker tag guestbook:v1 us.icr.io/REGISTRY_NAMESPACE/guestbook:v1
docker push us.icr.io/REGISTRY_NAMESPACE/guestbook:v1
```
Use the registry region and namespace assigned to your account/lab; do not assume `us.icr.io` is correct for every environment.

## Deploy
Update the image field in `deployment.yml`, then:
```bash
kubectl apply -f deployment.yml
kubectl get deployments,pods,svc
```

## Autoscaling
Apply `hpa.yml` after the Deployment exists:
```bash
kubectl apply -f hpa.yml
kubectl get hpa
kubectl get pods -w
```
An HPA cannot scale a Deployment from zero replicas in every configuration; behavior depends on Kubernetes version and HPA setup. Follow the exact course lab instructions for the requested zero-replica checkpoint and scaling exercise.

## Rolling update and rollback
After building/pushing the v2 image and updating the Deployment image:
```bash
kubectl apply -f deployment.yml
kubectl rollout status deployment/guestbook
kubectl rollout history deployment/guestbook
kubectl rollout undo deployment/guestbook
kubectl get rs
```
Keep the actual terminal output from your own lab for submission.
