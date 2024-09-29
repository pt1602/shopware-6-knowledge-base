# How to deploy a shopware 6 setup with gitlab

> ⚠️ **Warning:** Work in progress.

## Requirements

* Composer managed setup like [this](https://github.com/pt1602/shopware-docker-ddev)
* The prepared [file](gitlab-ci.yml)

---

## Preparation

* Create an ssh key pair somewhere on your system
* Here is one version how to create one

```shell
ssh-keygen -t ed25519 -a 420 -f ./my/cool/dir/id_ed25519 -C "deployment@myworkmail.de"
```

* Add the public key to authorized keys on your server

---

## Configuration

* Create a deploy token
    * Navigate to `Repository > Deploy Token`
    * Click on `Add token`
    * Create a token with read access
      ![deploy-token.png](imgs/deploy-token.png)
* Clone the repository on the server
    * `git clone https://tokenName:tokenPassword@https://gitlab.com/repo.git`
* Define CI/CD variables in gitlab
    * Navigate to `CI/CD > Variables`
    * Create the following variables and make sure to uncheck `Protect variable`
        * `SSH_CONNECTION` something like `user@127.0.0.1`
        * `SSH_PRIVATE_KEY` the private key of the before created key pair
* Add this [gitlab-ci.yml](gitlab-ci.yml) to your project
    * Make sure to replace
        * `/root-shopdir-dev/`
        * `/root-shopdir-live/`
    * And maybe also your branch in line seven `- if: '$CI_COMMIT_REF_NAME == "dev"'`
* Create a Merge Request into your dev/staging branch and hope it works 😂

