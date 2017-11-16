# ChefDK with Kitchen Google Cloud Plataform

#  Docker image

Supported tags and respective Dockerfile links

Base Image    |     Tag     |  Backed |  Dockerfile      |  Status
------------|-------------|--------|------------------|-------------------------------------
ubuntu:16.04   | latest      |  chefdf=2.3.4  cloud-sdk/ gcloud=178.0.0 |( [ Dockerfile ](https://github.com/petersonwsantos/chefdk_kitchen-google/blob/Dockerfile) ) | [![](https://images.microbadger.com/badges/image/petersonwsantos/chefdk_kitchen-google.svg)](https://microbadger.com/images/petersonwsantos/chefdk_kitchen-google "Get your own image badge on microbadger.com")


```
$ docker run -it --name chef_playground \
-v ~/.config/gcloud:/root/.config/gcloud \
-v ~/.ssh:/root/.ssh \
--mount type=bind,source="$(pwd)",target=/cookbook \
petersonwsantos/chefdk_kitchen-google
```
