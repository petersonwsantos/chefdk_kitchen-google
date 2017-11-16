# ChefDK with Kitchen Google Cloud Plataform

#  Docker image

Supported tags and respective Dockerfile links

Base Image    |     Tag     |  Backed |  Dockerfile      |  Status
------------|-------------|--------|------------------|-------------------------------------
ubuntu:16.04   | latest      |  chefdf=2.3.4  cloud-sdk/ gcloud=178.0.0 |( [ Dockerfile ](https://github.com/petersonwsantos/chefdk_kitchen-google/blob/master/Dockerfile) ) | [![](https://images.microbadger.com/badges/image/petersonwsantos/chefdk_kitchen-google.svg)](https://microbadger.com/images/petersonwsantos/chefdk_kitchen-google "Get your own image badge on microbadger.com")



How to Use: 
```
$ cd my_dev_code/

$ docker run -it --name chef_playground \
   -v ~/.config/gcloud:/root/.config/gcloud \
   -v ~/.ssh:/root/.ssh \
   --mount type=bind,source="$(pwd)",target=/cookbook \
    petersonwsantos/chefdk_kitchen-google
```
Explanation command above:

   Creates a volume for my gcloud credentials created earlier in my notebook.
   If you prefer you can take this line and run "gcloud init" directly in the container.
   ```
    -v ~/.config/gcloud:/root/.config/gcloud \
   ```
   Creates volume for my authentication key, that will be used in ".kitchen.yml"
   ( ssh_key:~/.ssh/key_google_compute_engine).
   ```
    -v ~/.ssh:/root/.ssh \
   ```
   Mount volume for my cookbooks's code ( $ cd my_dev_code/ ).    
   ```
   --mount type=bind,source="$(pwd)",target=/cookbook \
```


.kitchen.yml

```yaml 
---
driver:
  name: gce
  # Google Cloud Plataform - Project ID  <---------------------------
  project: Project-666
  zone: us-west1-c
  # Google Cloud Plataform - LOgin        <----------------------------
  email: Your_Login_GCE@gmail.com
  machine_type: g1-small
  tags:
    - devteam
    - test-kitchen
  service_account_scopes:
    - devstorage.read_write
    - userinfo.email

provisioner:
  name: chef_zero

verifier:
  name: inspec

transport:
  # Google Cloud Plataform - Enter Compute Engine / Metadata / add USER and SSH KEY    <------------------------------------
  # User
  username: login_of_metadata_key
  # Key 
  ssh_key:
    - ~/.ssh/key_google_compute_engine

platforms:
  - name: ubuntu-16.04
    driver:
      image_project: ubuntu-os-cloud
      image_family: ubuntu-1604-lts
      metadata:
        application: ubuntu
        release: a
        version: 1604


```
