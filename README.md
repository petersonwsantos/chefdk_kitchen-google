# ChefDK with Kitchen Google Cloud Plataform

#  Docker image

Supported tags and respective Dockerfile links

Base Image    |     Tag     |  Backed |  Dockerfile      |  Status
------------|-------------|--------|------------------|-------------------------------------
ubuntu:16.04   | latest      |  chefdf=2.3.4  cloud-sdk/ gcloud=178.0.0 |( [ Dockerfile ](https://github.com/petersonwsantos/chefdk_kitchen-google/blob/master/Dockerfile) ) | [![](https://images.microbadger.com/badges/image/petersonwsantos/chefdk_kitchen-google.svg)](https://microbadger.com/images/petersonwsantos/chefdk_kitchen-google "Get your own image badge on microbadger.com")


```
$ docker run -it --name chef_playground \
-v ~/.config/gcloud:/root/.config/gcloud \
-v ~/.ssh:/root/.ssh \
--mount type=bind,source="$(pwd)",target=/cookbook \
petersonwsantos/chefdk_kitchen-google
```

Example:
.kitchen.yml

```yaml 
---
driver:
  name: gce
  # Project ID - Google Cloud Plataform  <---------------------------
  project: Project-666
  zone: us-west1-c
  # Login - Google Cloud Plataform        <----------------------------
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
  # Google Cloud Plataform / Metadata / USER and SSH KEY    <------------------------------------
  # User
  username: login_yor_key
  # Key (path public Key)
  ssh_key:
    - ~/.ssh/google_compute_engine

platforms:
  - name: ubuntu-16.04
    driver:
      image_project: ubuntu-os-cloud
      image_family: ubuntu-1604-lts
      metadata:
        application: ubuntu
        release: a
        version: 1604

suites:
  - name: default
    run_list:
      - recipe[apache::default]
    verifier:
      inspec_tests:
        - test/recipes
    attributes:
```
