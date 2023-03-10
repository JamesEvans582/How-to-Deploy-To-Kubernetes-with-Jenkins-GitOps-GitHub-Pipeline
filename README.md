# How-to-Deploy-To-Kubernetes-with-Jenkins-GitOps-GitHub-Pipeline
Create Real World CI CD Pipeline using Jenkins and GitOps (ArgoCD) to dockerize your code, and deploy the container into a Kubernetes cluster.

This tutorial is following cloud with Raj -> https://www.youtube.com/watch?v=o4QG_kqYvHk&t=812s&ab_channel=CloudWithRaj

The work flow. 
- We will work on a code App.py 
- Push the code to Github repo named 'Kubernetescode'
- As soon as we push the code a Jenkinsjob get triggered, which build Docker container image
- This will be save in a container registry (DockerHub) which is named test:10 
- 10 will be the tag, updates will increase the number tag
- Jenkins will also trigger a manifest yaml file to update the image 
- we will be using Gitops (Argo) to monitor repo. 
- This will then grab the update or aadjustments and deploy them to the Kubernetes cluster. 

prerequisite
- you must have Jenkins installed on a ec2 (how to link -> https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/) if you are struggling this fella can help you out -> https://www.youtube.com/watch?v=Hz2QJ420LPE&ab_channel=SandipDas

- You must have the correct plugins | link to cloud with Raj github page -> https://github.com/saha-rajdeep/kubernetescode

- You must have argo (how to you -> https://argo-cd.readthedocs.io/en/stable/getting_started/) if you are struggling techworld with nana can help -> https://www.youtube.com/watch?v=MeU5_k9ssrs&t=1853s&ab_channel=TechWorldwithNana

So if you have followed this correctly you should have ...

<img width="1792" alt="Screenshot 2023-03-01 at 18 03 20" src="https://user-images.githubusercontent.com/71371405/222225391-e83578ea-e9f2-4439-a6ad-b71a3757c4dd.png">


Jenkins running on an EC2 Server, with all the plugins! 

<img width="1792" alt="Screenshot 2023-03-01 at 18 03 37" src="https://user-images.githubusercontent.com/71371405/222225650-a21faf9c-7b18-4e7c-85a4-6ea5dcde8471.png">

Argo installed via minikube / kubectl 

1) Firstly, well done so far. The next stage now, is to set the Credentials for DockerHub and GitHub on Jenkins. This is because we will run DockerHub as our repository. 

- Jenkins Dashboard ->  Manage Jenkins -> Manage Credentials -> under global credentials -> add credentials 
<img width="1792" alt="Screenshot 2023-03-01 at 18 28 33" src="https://user-images.githubusercontent.com/71371405/222230974-7e62660f-a6f8-4cd2-a0be-9a7cbfd386fd.png">

- Add another credentials -> Github -> your account name -> we will need to generate a token from Github itself. 

<img width="1792" alt="Screenshot 2023-03-01 at 18 35 51" src="https://user-images.githubusercontent.com/71371405/222234111-5d4ce133-da5c-4c57-976f-7c323775efd2.png">

- now we need to generate our Github token...

profile

<img width="1792" alt="Screenshot 2023-03-01 at 18 40 05" src="https://user-images.githubusercontent.com/71371405/222235549-5d5add94-cf93-4a07-be3a-e08b98d48e6e.png">

- settings -> developer settings -> token  
<img width="1792" alt="Screenshot 2023-03-01 at 18 40 35" src="https://user-images.githubusercontent.com/71371405/222235878-6d1486f4-f842-4216-bf7a-df3d83939751.png">

Select -> repo -> webhook -> notifications 

<img width="1792" alt="Screenshot 2023-03-01 at 18 43 13" src="https://user-images.githubusercontent.com/71371405/222236180-f1a9e89f-b371-4e6c-b913-d3f8dc829b17.png">

Generate token -> copy token -> place as password into Jenkins 


<img width="1792" alt="Screenshot 2023-03-01 at 18 52 28" src="https://user-images.githubusercontent.com/71371405/222236916-264868ee-0266-4230-8080-1a1681bf492b.png">

- Next stage 

- Jenkins dashboard  -> new item -> name buildimage -> select pipeline -> ok 

<img width="1792" alt="Screenshot 2023-03-01 at 18 54 31" src="https://user-images.githubusercontent.com/71371405/222241602-1550be58-6e8d-49ac-b84f-8e6af832160a.png">

<img width="1792" alt="Screenshot 2023-03-01 at 19 00 33" src="https://user-images.githubusercontent.com/71371405/222241663-fbcf879d-c2d8-4255-9b82-2e429c949bc5.png">

<img width="1792" alt="Screenshot 2023-03-01 at 19 01 13" src="https://user-images.githubusercontent.com/71371405/222241723-e62032ca-a9ee-4181-ba19-e531745d6bee.png">

Create new pipeline -> call it updatemanifest -> 


<img width="1792" alt="Screenshot 2023-03-01 at 19 14 55" src="https://user-images.githubusercontent.com/71371405/222242040-c8fe8728-c931-4531-bec0-785dc4513839.png">













