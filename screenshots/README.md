# Screenshots
To help review your infrastructure, please include the following screenshots in this directory::

## Deployment Pipeline
### DockerHub showing containers that you have pushed

<img width="1440" alt="Screenshot 2022-05-23 at 01 25 07" src="https://user-images.githubusercontent.com/80678596/169720544-c3adde93-2a47-497f-83d2-8e42014e29cd.png">


* GitHub repository’s settings showing your Travis webhook (can be found in Settings - Webhook)

### Gitlab showing a successful build and deploy job


<img width="1440" alt="Screenshot 2022-05-22 at 03 16 24" src="https://user-images.githubusercontent.com/80678596/169674240-a4136520-0081-44c6-8d6e-1836090bc43c.png">


<img width="1105" alt="Screenshot 2022-05-22 at 02 40 23" src="https://user-images.githubusercontent.com/80678596/169673602-36b2d64f-3e5c-4965-9575-d07578a4ee31.png">


<img width="1435" alt="Screenshot 2022-05-23 at 21 39 41" src="https://user-images.githubusercontent.com/80678596/169893848-8ccd156c-69de-4316-97c4-88b483ec4a0c.png">


<img width="866" alt="Screenshot 2022-05-22 at 03 15 08" src="https://user-images.githubusercontent.com/80678596/169674193-a3377703-7821-41d8-aee8-64942fd5795b.png">

## Kubernetes
### To verify Kubernetes pods are deployed properly

                    kubectl get pods

### To verify Kubernetes services are properly set up


<img width="1304" alt="Screenshot 2022-05-23 at 19 08 44" src="https://user-images.githubusercontent.com/80678596/169885491-9b87bb95-03d1-446d-9734-3879ac8eea9f.png">


                    kubectl describe services

### To verify that you have horizontal scaling set against CPU usage


<img width="809" alt="Screenshot 2022-05-23 at 18 58 28" src="https://user-images.githubusercontent.com/80678596/169884400-b6a5981c-d607-4b74-9202-01ef312e63de.png">

<img width="642" alt="Screenshot 2022-05-23 at 18 58 37" src="https://user-images.githubusercontent.com/80678596/169884408-d562309e-6744-4e65-9f2c-850e5b8ab4f6.png">

<img width="541" alt="Screenshot 2022-05-23 at 18 58 47" src="https://user-images.githubusercontent.com/80678596/169884413-1e5d58a8-84ae-4522-9b34-33b4aafbf403.png">

<img width="596" alt="Screenshot 2022-05-23 at 18 59 03" src="https://user-images.githubusercontent.com/80678596/169884416-60a11282-800a-4a96-ad4d-c6581b2fb386.png">

<img width="844" alt="Screenshot 2022-05-23 at 18 59 14" src="https://user-images.githubusercontent.com/80678596/169884421-e08a6fa6-0f1e-4b70-ae8a-86f02d89f31f.png">


                        kubectl describe hpa

<img width="872" alt="Screenshot 2022-05-23 at 20 29 28" src="https://user-images.githubusercontent.com/80678596/169884213-047764fe-b6e2-4275-9d0b-3269b0d25a47.png">

<img width="870" alt="Screenshot 2022-05-23 at 20 29 47" src="https://user-images.githubusercontent.com/80678596/169884142-fc54c2f5-22b5-4dd4-8051-50d53082b8e4.png">

<img width="880" alt="Screenshot 2022-05-23 at 20 30 02" src="https://user-images.githubusercontent.com/80678596/169884060-15fa9bfb-65da-49c5-9936-a677f513985e.png">

<img width="883" alt="Screenshot 2022-05-23 at 20 30 16" src="https://user-images.githubusercontent.com/80678596/169883982-6cdfe4c1-cb85-4948-9a5c-61c79818c5bd.png">

###  To verify that you have set up logging with a backend application

                        kubectl logs {pod_name}

<img width="1021" alt="Screenshot 2022-05-23 at 20 18 44" src="https://user-images.githubusercontent.com/80678596/169882318-e5629d26-bc00-4a29-8f9c-4bc767931173.png">


###  The finall end point image

<img width="1440" alt="Screenshot 2022-05-23 at 19 38 38" src="https://user-images.githubusercontent.com/80678596/169885764-efa2bbed-5cfe-40ec-8185-d0241e7b5f1c.png">
