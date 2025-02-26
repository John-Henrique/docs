---
id: installer
title: Amazon Web Services Installer
sidebar_label: Installer
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

On this page, we explain step by step how to install **CloudPanel** on an EC2 instance on [Amazon Web Services](https://aws.amazon.com/).

## Launching an EC2 Instance

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/ec2/). 

2. Go to the **EC2 Service**, and click on **Launch Instances**.

<img class="border" alt="Click on the Launch Instances Button" src={useBaseUrl('img/getting-started/amazon-web-services/click-on-launch-instance-button.png')} />

### Name and tags

Enter the name of your **EC2 Instance**, e.g., **my-cloudpanel-instance**.

<img class="border" alt="Name and Tags" src={useBaseUrl('img/getting-started/amazon-web-services/name-and-tags.png')} />

### Choose Operating System

1. Select **Ubuntu 22.04** or **Debian 11** as **OS Image**. Both **Architectures** **x86** and **ARM** are supported by **CloudPanel**.

<img class="border" alt="OS Image" src={useBaseUrl('img/getting-started/amazon-web-services/os-image.png')} />

### Instance Type

Choose an **instance type** and ensure that it fits the [minimum requirements](../../../../requirements).

<img alt="Instance Type" class="border" src={useBaseUrl('img/getting-started/amazon-web-services/instance-type.png')} />

### Key pair (login)

Select a **Key pair** or [Create a new key pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html?icmpid=docs_ec2_console) to log in via **SSH** after launching the **instance**.

<img alt="Key Pair" class="border" src={useBaseUrl('img/getting-started/amazon-web-services/key-pair.png')} />

### Network settings

1. Click on **Edit** to make changes on the **Network Settings**.

<img alt="Edit Network Settings" class="border" src={useBaseUrl('img/getting-started/amazon-web-services/network-settings-edit.png')} />

2. Select the **VPC**, **Subnet**, and enter a **Security Group Name** and **Description**.

<img alt="Edit Network Settings" class="border" src={useBaseUrl('img/getting-started/amazon-web-services/network-settings-security-group-name.png')} />

#### Inbound security groups rules

:::warning CloudPanel Firewall
All pre-configured [CloudPanel Firewall Rules](../../../../admin-area/security/#firewall) are not needed and should be removed. <br />
If you want to use the **CloudPanel** integrated firewall for whitelisting ports, create a **security group** with one rule which allows **All TCP**.
In that case, all traffic is filtered by the [CloudPanel Firewall](../../../../admin-area/security/#firewall) and not by **AWS**.
:::

Create a **Security Group** with the following rules:

- **SSH (22)** - For your IP only
- **HTTP (80)** - For everyone
- **HTTPS (443)** - For everyone
- **CloudPanel (8443)** - For your IP only

<img alt="Inbound security groups rules" class="border" src={useBaseUrl('img/getting-started/amazon-web-services/network-settings-inbound-rules.png')} />

### Configure Storage

Configure as minimum **10 GB** disk size and select **gp3** (Latest SSD generation).

<img alt="Configure Storage" class="border" src={useBaseUrl('img/getting-started/amazon-web-services/installer-configure-storage.png')} />

### Launch Instance

Click on the button **Launch Instance** to launch the **instance**.

<img alt="Launch Instance" class="border" src={useBaseUrl('img/getting-started/amazon-web-services/launch-instance.png')} />

## Create Elastic IP Address

A static IP ([Elastic IP Address](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)) is needed for running web applications. <br />

1. To create an **Elastic IP Address** click in the left navigation on **Network & Security** --> **Elastic IPs**.

2. Click on button **Allocate Elastic IP address** to create an **Elastic IP Address**.

3. Select the **Allocated IP Address** and **Associate** it to your launched instance.

<img alt="Associate Elastic IP Address" class="border" src={useBaseUrl('img/getting-started/amazon-web-services/associate-eip.png')} />

## Install CloudPanel

After launching the **EC2 Instance**, log in with **SSH** and run the installer script.

<Tabs
defaultValue="ubuntu-22.04"
values={[
{ label: 'Ubuntu 22.04 LTS', value: 'ubuntu-22.04', },
{ label: 'Debian 11 LTS', value: 'debian-11', },
]}>
<TabItem value="ubuntu-22.04">

1. Login via **SSH** to the **EC2 Instance**.

```bash
ssh -i path_to_your_private_key.pem ubuntu@yourElasticIpAddress
```

2. Switch to the **root** user:

```bash
sudo su root
```

3. Update the system and install the required packages.

```bash
apt update && apt -y upgrade && apt -y install curl wget sudo
```

4. Run the installer with your preferred **Database Engine**.

<Tabs
defaultValue="ubuntu-mysql-8.0"
values={[
{ label: 'MySQL 8.0', value: 'ubuntu-mysql-8.0', },
{ label: 'MariaDB 10.9', value: 'ubuntu-mariadb-10.9', },
{ label: 'MariaDB 10.8', value: 'ubuntu-mariadb-10.8', },
{ label: 'MariaDB 10.6', value: 'ubuntu-mariadb-10.6', },
]}>
<TabItem value="ubuntu-mysql-8.0">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=aws bash
```

</TabItem>
<TabItem value="ubuntu-mariadb-10.9">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=aws DB_ENGINE=MARIADB_10.9 bash
```

</TabItem>
<TabItem value="ubuntu-mariadb-10.8">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=aws DB_ENGINE=MARIADB_10.8 bash
```

</TabItem>
<TabItem value="ubuntu-mariadb-10.6">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=aws DB_ENGINE=MARIADB_10.6 bash
```

</TabItem>
</Tabs>

</TabItem>
<TabItem value="debian-11">

1. Login via **SSH** to the **EC2 Instance**.

```bash
ssh -i path_to_your_private_key.pem admin@yourElasticIpAddress
```

2. Switch to the **root** user:

```bash
sudo su root
```

3. Update the system and install the required packages.

```bash
apt update && apt -y upgrade && apt -y install curl wget sudo
```

4. Run the installer with your preferred **Database Engine**.

<Tabs
defaultValue="debian-mysql-8.0"
values={[
{ label: 'MySQL 8.0', value: 'debian-mysql-8.0', },
{ label: 'MySQL 5.7', value: 'debian-mysql-5.7', },
{ label: 'MariaDB 10.9', value: 'debian-mariadb-10.9', },
{ label: 'MariaDB 10.8', value: 'debian-mariadb-10.8', },
{ label: 'MariaDB 10.7', value: 'debian-mariadb-10.7', },
]}>
<TabItem value="debian-mysql-8.0">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=aws bash
```

</TabItem>
<TabItem value="debian-mysql-5.7">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=aws DB_ENGINE=MYSQL_5.7 bash
```

</TabItem>
<TabItem value="debian-mariadb-10.9">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=aws DB_ENGINE=MARIADB_10.9 bash
```

</TabItem>
<TabItem value="debian-mariadb-10.8">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=aws DB_ENGINE=MARIADB_10.8 bash
```

</TabItem>
<TabItem value="debian-mariadb-10.7">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=aws DB_ENGINE=MARIADB_10.7 bash
```

</TabItem>
</Tabs>

</TabItem>
</Tabs>

## Access CloudPanel

You can now access **CloudPanel** via Browser: **https://yourElasticIpAddress:8443**

Ignore the self-signed certificate warning and click on **Advanced** and **Proceed** to continue to **CloudPanel**.

<img alt="Ignore Self-Signed Certificate" class="border" src={useBaseUrl('img/getting-started/ignore-self-signed-certificate.png')} />