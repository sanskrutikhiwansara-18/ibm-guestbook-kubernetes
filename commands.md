# Command checklist for the 10 submission tasks

Run these in the terminal provided by your IBM Skills Network lab, adapting names/paths to match the lab.

## Task 1 — Dockerfile
```bash
cat Dockerfile
```
This project Dockerfile includes `COPY` and `EXPOSE`.

## Task 2 — Registry image tagged v1
```bash
ibmcloud cr images
```
Save the actual output that shows your pushed `guestbook:v1` image.

## Task 3 — Default title and heading
```bash
grep -E '<title>|<h1>' index.html
```

## Task 4 — HPA state
```bash
kubectl get hpa
```
The rubric mentions an HPA with zero replicas. Follow the lab's exact steps; this starter HPA uses `minReplicas: 1` for safer general behavior.

## Task 5 — Autoscaling evidence
```bash
kubectl get hpa
kubectl get deployment
kubectl get pods
```
Capture output after replicas have genuinely increased.

## Task 6 — Push updated image and final digest
Build/tag/push the updated image as instructed by your lab. Example:
```bash
docker build -t guestbook:v2 -f Dockerfile .
docker tag guestbook:v2 us.icr.io/REGISTRY_NAMESPACE/guestbook:v2
docker push us.icr.io/REGISTRY_NAMESPACE/guestbook:v2
```
Save the complete real push output including the digest.

## Task 7 — Apply deployment
```bash
kubectl apply -f deployment.yml
```
Save the actual confirmation output.

## Task 8 — Updated title and heading
To use the v2 HTML, copy it over the default file before building the v2 image:
```bash
cp index-v2.html index.html
grep -E '<title>|<h1>' index.html
```
Expected source text: `Guestbook – v2` in both title and heading.

## Task 9 — Rollout history
```bash
kubectl rollout history deployment/guestbook
```
Use the deployment name from your course lab and ensure the revisions were created by real deployment updates.

## Task 10 — ReplicaSets after rollback
```bash
kubectl rollout undo deployment/guestbook
kubectl rollout status deployment/guestbook
kubectl get rs
```
Capture the real output after rollback.
