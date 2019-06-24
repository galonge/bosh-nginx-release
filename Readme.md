# BOSH nginx release


### Setup

#### Pre-requisites

To use this nginx release, you should have a Bosh Director setup and a stemcell uploaded to it.
This release has been tested on an ubuntu-xenial stemcell.

To install a bosh director, follow the instructions here. a virtual box environment should do: <https://bosh.io/docs/bosh-lite>;

Upload Ubuntu Xenial stemcell to Bosh

```bash
bosh -e {{env-alias}} upload-stemcell --sha1 674cd3c1e64d8c51e62770697a63c07ca04e9bbd \
  https://bosh.io/d/stemcells/bosh-warden-boshlite-ubuntu-xenial-go_agent?v=315.45
```

####  Uploading the release to Bosh Director

There are two ways this release can be added to your bosh director.

1. From Repo Release Files (Clone Repo)
  ```bash
    git clone https://github.com/wayneskillz/bosh-nginx-release.git
    cd bosh-nginx-release
    bosh upload-release
  ```
2. From Release Tarball (Located in the tarball directory)
  ```bash
    bosh -e {{env_alias}} upload-release https://github.com/wayneskillz/bosh-nginx-release/tarball/nginx-1.13.1.tar.gz
  ```

#### Deploying the Nginx release

Assuming you are in the bosh nginx directory cloned earlier, i.e. in the bosh-nginx-release directory:

```bash
bosh -e {{env_alias}} -d nginx-deployment deploy examples/nginx-deployment.yml
```

#### Testing

Visit <http://10.244.0.2/>; on your browser and you should see the nginx homescreen with a popup to authenticate:

Default username and password is `admin`

After entering this, you should see the default nginx homepage.



## Additional Notes

#### 1. Locate your vm ip

* In the event that this release was not deployed on a fresh virtualbox vm, type the following command to view the ip address for the deployment.

```bash
bosh -e {{env_alias}} -d nginx-deployment vms
```

Now open your browser at that ip to test.

*Note* Replace {{env_alias}} with the alias name of your bosh director.
