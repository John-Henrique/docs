---
id: installer
title: Digital Ocean Installer
sidebar_label: Installer
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

On this page, we explain step by step how to install **CloudPanel** on [Digital Ocean](https://www.digitalocean.com/).

## Launching a Droplet

1. Login to your [Digital Ocean](https://cloud.digitalocean.com/login) account. 

2. In the left navigation, click on **Droplets** and then on **Create Droplet**.

### Choose an image

Select **Ubuntu 22.04** or **Debian 11** as **OS Image**.

<img class="border" alt="Choose an image" src={useBaseUrl('img/getting-started/digital-ocean/choose-image.png')} />

### Droplet Size

Choose the size of your **Droplet**, e.g., **Premium AMD with NVMe SSD**.

<img class="border" alt="Droplet Size" src={useBaseUrl('img/getting-started/digital-ocean/droplet-size.png')} />

### Datacenter Region

Choose the **Datacenter Region** where you want to run your **Droplet**.

<img class="border" alt="Datacenter Region" src={useBaseUrl('img/getting-started/digital-ocean/datacenter-region.png')} />

### Authentication Method

Select your **Authentication Method**, **SSH keys** or **Password**. <br />
How to create an SSH Key, is explained on the site: [How-to Add SSH Keys to New or Existing Droplets](https://www.digitalocean.com/docs/droplets/how-to/add-ssh-keys/)

<img class="border" alt="Authentication Method" src={useBaseUrl('img/getting-started/digital-ocean/authentication-method.png')} />

### Finalize and Create

Enter a **hostname**, and click on the button **Create Droplet** to launch your **Droplet**.

<img class="border" alt="Finalize and Create" src={useBaseUrl('img/getting-started/digital-ocean/finalize-and-create.png')} />

## Assigning a Reserved IP

A **Reserved IP** (static ip) is highly recommended to have the same IP after changing the size of your **Droplet**.

To create a **Reserved IP**, do the following steps:

1. In the left navigation, click on **Networking**.

2. Select your **Droplet** and click on the button **Assign Reserved IP**.

<img class="border" alt="Assigning a Reserved IP" src={useBaseUrl('img/getting-started/digital-ocean/assigning-a-reserved-ip.png')} />

## Install CloudPanel

After launching the **Droplet**, log in with **SSH** and run the installer script.

<Tabs
defaultValue="ubuntu-22.04"
values={[
{ label: 'Ubuntu 22.04 LTS', value: 'ubuntu-22.04', },
{ label: 'Debian 11 LTS', value: 'debian-11', },
]}>
<TabItem value="ubuntu-22.04">

1. Login via **SSH** to the **Droplet**.

```bash
ssh -i path_to_your_private_key root@yourIpAddress
```

2. Update the system and install the required packages.

```bash
apt update && apt -y upgrade && apt -y install curl wget sudo
```

3. Run the installer with your preferred **Database Engine**.

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
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=do bash
```

</TabItem>
<TabItem value="ubuntu-mariadb-10.9">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=do DB_ENGINE=MARIADB_10.9 bash
```

</TabItem>
<TabItem value="ubuntu-mariadb-10.8">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=do DB_ENGINE=MARIADB_10.8 bash
```

</TabItem>
<TabItem value="ubuntu-mariadb-10.6">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=do DB_ENGINE=MARIADB_10.6 bash
```

</TabItem>
</Tabs>

</TabItem>
<TabItem value="debian-11">

1. Login via **SSH** to the **Droplet**.

```bash
ssh -i path_to_your_private_key root@yourIpAddress
```

2. Update the system and install the required packages.

```bash
apt update && apt -y upgrade && apt -y install curl wget sudo
```

3. Run the installer with your preferred **Database Engine**.

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
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=do bash
```

</TabItem>
<TabItem value="debian-mysql-5.7">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=do DB_ENGINE=MYSQL_5.7 bash
```

</TabItem>
<TabItem value="debian-mariadb-10.9">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=do DB_ENGINE=MARIADB_10.9 bash
```

</TabItem>
<TabItem value="debian-mariadb-10.8">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=do DB_ENGINE=MARIADB_10.8 bash
```

</TabItem>
<TabItem value="debian-mariadb-10.7">

```bash
curl -sSL https://installer.cloudpanel.io/ce/v2/install.sh | sudo CLOUD=do DB_ENGINE=MARIADB_10.7 bash
```

</TabItem>
</Tabs>

</TabItem>
</Tabs>

## Access CloudPanel

You can now access **CloudPanel** via Browser: **https://yourIpAddress:8443**

Ignore the self-signed certificate warning and click on **Advanced** and **Proceed** to continue to **CloudPanel**.

<img alt="Ignore Self-Signed Certificate" class="border" src={useBaseUrl('img/getting-started/ignore-self-signed-certificate.png')} />
