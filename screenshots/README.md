# Screenshots
To help review your infrastructure, please include the following screenshots in this directory::

## Deployment Pipeline
* DockerHub showing containers that you have pushed

<img width="1381" alt="Screenshot 2022-05-22 at 03 13 41" src="https://user-images.githubusercontent.com/80678596/169674169-a3ee191d-ac14-47f6-9c26-326d466f9258.png">

* GitHub repository’s settings showing your Travis webhook (can be found in Settings - Webhook)

* Travis CI showing a successful build and deploy job


<img width="1440" alt="Screenshot 2022-05-22 at 03 16 24" src="https://user-images.githubusercontent.com/80678596/169674240-a4136520-0081-44c6-8d6e-1836090bc43c.png">


<img width="1105" alt="Screenshot 2022-05-22 at 02 40 23" src="https://user-images.githubusercontent.com/80678596/169673602-36b2d64f-3e5c-4965-9575-d07578a4ee31.png">


<img width="866" alt="Screenshot 2022-05-22 at 03 15 08" src="https://user-images.githubusercontent.com/80678596/169674193-a3377703-7821-41d8-aee8-64942fd5795b.png">

## Kubernetes
* To verify Kubernetes pods are deployed properly
```bash
kubectl get pods
```
* To verify Kubernetes services are properly set up
```bash
kubectl describe services
```
* To verify that you have horizontal scaling set against CPU usage
```bash
kubectl describe hpa
```
* To verify that you have set up logging with a backend application
```bash
kubectl logs {pod_name}
```
