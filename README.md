# ![Foodie CSTAD logo Logo](https://cdn-icons-png.flaticon.com/512/5978/5978671.png) Foodie CSTAD

Foodie CSTAD is probably the most modern and sophisticated insecure web application! It can be used in security
trainings, awareness demos, CTFs and as a guinea pig for security tools! Juice Shop encompasses vulnerabilities from the
entire
[Foodie CSTAD](https://github.com/CybersecurityTeam-CSTAD/foodie_shop_clone.git) along with many other security flaws found in real-world
applications!

![Foodie CSTAD show screenshot](<img width="952" alt="Screenshot 2024-01-01 152651" src="https://github.com/CybersecurityTeam-CSTAD/foodie_shop_clone/assets/126130178/39f37622-3987-409e-9e28-0e136ca89ad9">
)

For a detailed introduction, full list of features and architecture overview please visit the official project page:
<https://food.cstad.shop>

## Table of contents

- [Setup](#setup)
    - [From Sources](#from-sources)
    - [Packaged Distributions](#packaged-distributions)
    - [Docker Container](#docker-container)
    - [Amazon EC2 Instance](#amazon-ec2-instance)
    - [Google Compute Engine Instance](#google-compute-engine-instance)
- [Demo](#demo)
- [Documentation](#documentation)
    - [Node.js version compatibility](#nodejs-version-compatibility)
    - [Troubleshooting](#troubleshooting)
    - [Official companion guide](#official-companion-guide)
- [Contributing](#contributing)
- [References](#references)
- [Merchandise](#merchandise)
- [Donations](#donations)
- [Contributors](#contributors)
- [Licensing](#licensing)

## Setup
### From Sources

![GitHub repo size](https://img.shields.io/github/repo-size/juice-shop/juice-shop.svg)

1. Install [node.js](#nodejs-version-compatibility)
2. Run `git clone https://github.com/CybersecurityTeam-CSTAD/foodie_shop_clone.git` 
3. Go into the cloned folder with `cd foodie_shop_clone`
4. Run `npm install` (only has to be done before first start or when you change the source code)
5. Run `npm start`
6. Browse to <http://localhost:3000>

### Docker Container

[![Docker Pulls](https://d36jcksde1wxzq.cloudfront.net/saas-mega/blueFingerprint.png?d=https%3A%2F%2Fd36jcksde1wxzq.cloudfront.net%2Fsaas-mega%2FblueFingerprint.png)](https://hub.docker.com/repository/docker/sokpheng001/cstad-shop/)

1. Install [Docker](https://www.docker.com)
2. Run `docker pull sokpheng001/cstad-shop:latest`
3. Run `docker run -dp 3000:3000 sokpheng001/cstad-shop:latest`
4. Browse to <http://localhost:3000> (on macOS and Windows browse to
   <http://192.168.99.100:3000> if you are using docker-machine instead of the native docker installation)
   
### Amazon EC2 Instance

1. In the _EC2_ sidenav select _Instances_ and click _Launch Instance_
2. In _Step 1: Choose an Amazon Machine Image (AMI)_ choose an _Amazon Linux AMI_ or _Amazon Linux 2 AMI_
3. In _Step 3: Configure Instance Details_ unfold _Advanced Details_ and copy the script below into _User Data_
4. In _Step 6: Configure Security Group_ add a _Rule_ that opens port 80 for HTTP
5. Launch your instance
6. Browse to your instance's public DNS

```
#!/bin/bash
yum update -y
yum install -y docker
service docker start
docker pull sokpheng001/cstad-shop:latest
docker run -dp 80:3000 sokpheng001/cstad-shop:latest
```

### Google Compute Engine Instance

1. Login to the Google Cloud Console and
   [open Cloud Shell](https://console.cloud.google.com/home/dashboard?cloudshell=true).
2. Launch a new GCE instance based on the juice-shop container. Take note of the `EXTERNAL_IP` provided in the output.

```
gcloud compute instances create-with-container owasp-juice-shop-app --container-image bkimminich/juice-shop
```

3. Create a firewall rule that allows inbound traffic to port 3000

```
gcloud compute firewall-rules create juice-rule --allow tcp:3000
```

4. Your container is now running and available at
   `http://<EXTERNAL_IP>:3000/`

### Heroku

1. [Sign up to Heroku](https://signup.heroku.com/) and
   [log in to your account](https://id.heroku.com/login)
2. Click the button below and follow the instructions

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

If you have forked the Juice Shop repository on GitHub, the _Deploy to
Heroku_ button will deploy your forked version of the application.

## Demo

Feel free to have a look at the latest version of OWASP Juice Shop:
<https://food.cstad.shop>

> This is a deployment-test and sneak-peek instance only! You are __not
> supposed__ to use this instance for your own hacking endeavours! No
> guaranteed uptime! Guaranteed stern looks if you break it!

## Documentation

### Node.js version compatibility

![GitHub package.json dynamic](https://img.shields.io/github/package-json/cpu/bkimminich/juice-shop)
![GitHub package.json dynamic](https://img.shields.io/github/package-json/os/bkimminich/juice-shop)

Foodie CSTAD officially supports the following versions of
[node.js](http://nodejs.org) in line with the official
[node.js LTS schedule](https://github.com/nodejs/LTS) as close as possible. Docker images and packaged distributions are
offered accordingly.

| node.js | Supported            | Tested                                                       | [Packaged Distributions](#packaged-distributions) | [Docker images](#docker-container) from `master` | [Docker images](#docker-container) from `develop` |
|:--------|:---------------------|:-------------------------------------------------------------|:--------------------------------------------------|:-------------------------------------------------|:--------------------------------------------------|
| 21.x    | :x:                  | :x:                                                          |                                                   |                                                  |                                                   |
| 20.x    | :heavy_check_mark:   | :heavy_check_mark:                                           | Windows (`x64`), MacOS (`x64`), Linux (`x64`)     |                                                  |                                                   |
| 20.6.0  | :x:                  | :bug: https://github.com/angular/angular-cli/issues/25782 |                                                   |                                                  |                                                   |
| 19.x    | (:heavy_check_mark:) | :x:                                                          |                                                   |                                                  |                                                   |
| 18.x    | :heavy_check_mark:   | :heavy_check_mark:                                           | Windows (`x64`), MacOS (`x64`), Linux (`x64`)     | `latest` (`linux/amd64`, `linux/arm64`)          | `snapshot` (`linux/amd64`, `linux/arm64`)         |
| 17.x    | (:heavy_check_mark:) | :x:                                                          |                                                   |                                                  |                                                   |
| 16.x    | :heavy_check_mark:   | :heavy_check_mark:                                           | Windows (`x64`), MacOS (`x64`), Linux (`x64`)     |                                                  |                                                   |
| <16.x   | :x:                  | :x:                                                          |                                                   |                                                  |                                                   |

Foodie CSTAD is automatically tested _only on the latest `.x` minor version_ of each node.js version mentioned above!
There is no guarantee that older minor node.js releases will always work with Juice Shop!
Please make sure you stay up to date with your chosen version.


## Contributors

The OWASP Juice Shop core project team are:

- [Kim Chansokpheng](https://github.com/sokpheng001) nick name `sokpheng001`
  ([Project Leader](https://twitter.com/SoPheng88402351))
- [Cheat Setha](https://github.com/CheatSetha) nick name `Cheat Setha`
- [Ngan Vidy](https://github.com/Vandy1100) nick name `Vandy1100`
- [Yoeurn Sonita](https://github.com/sonitayoeurn) nick name `sonitayoeurn`
- [Pao Ponareach](https://github.com/reachhwasup) nick name `sonitayoeurn`


## Licensing

[![license](https://img.shields.io/github/license/bkimminich/juice-shop.svg)](LICENSE)

This program is free software: you can redistribute it and/or modify it under the terms of the [MIT license](LICENSE).
OWASP Juice Shop and any contributions are Copyright © by Bjoern Kimminich & the OWASP Juice Shop contributors
2014-2023.

![Juice Shop Logo](https://raw.githubusercontent.com/bkimminich/juice-shop/master/frontend/src/assets/public/images/JuiceShop_Logo_400px.png)
