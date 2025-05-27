# Enabling Repository and Syncing Content to Red Hat Satellite

[Red Hat Satellite Learning Series Main Menu](https://github.com/rajatagrawal1094/RedHatSatellite)

## Table of Contents
- [Introduction](#introduction)
- [Enabling Repository using Red Hat Satellite Dashboard](#enabling-repository-using-red-hat-satellite-dashboard)
- [Synchronizing Content using Red Hat Satellite Dashboard](#synchronizing-content-using-red-hat-satellite-dashboard)
- [Enabling Repository using hammer CLI](#enabling-repository-using-hammer-cli)
- [Synchronizing Content using hammer CLI](#synchronizing-content-using-hammer-cli)
- [Summary](#summary)

## Enabling Repository using Red Hat Satellite Dashboard

Open a browser, enter the Red Hat Satellite Server URL - https://satellite.example.com

![dashboard](/images/1-dashboard.png)

Enter Credentials and click Log In button

- **Username**: admin
- **Password**: redhat

![login](/images/2-login.png)

Navigate to **Content > Red Hat Repositories**. You will now see all available repositories. 

![repositories](/images/3-repositories.png)

We will be enabling the following:

| Name        						     | Repository 					 |
| :--------------------------------------------------------: | :-----------------------------------------------: |
| Red Hat Enterprise Linux 8 for x86_64 - AppStream RPMs 8   | rhel-8-for-x86_64-appstream-rpms             	 |
| Red Hat Enterprise Linux 8 for x86_64 - BaseOS RPMs 8      | rhel-8-for-x86_64-baseos-rpms             	 |
| Red Hat Enterprise Linux 9 for x86_64 - AppStream RPMs 9.5 | rhel-9-for-x86_64-appstream-rpms             	 |
| Red Hat Enterprise Linux 8 for x86_64 - BaseOS RPMs 9.5    | rhel-9-for-x86_64-baseos-rpms             	 |
| Red Hat Satellite Capsule 6.15 for RHEL 8 x86_64 RPMs      | satellite-capsule-6.15-for-rhel-8-x86_64-rpms     |
| Red Hat Satellite Maintenance 6.15 for RHEL 8 x86_64 RPMs  | satellite-maintenance-6.15-for-rhel-8-x86_64-rpms |

In the search bar, search for the repository names (one at a time). Click on the drop down arrow on the left side to see the available architectures

![search](/images/4-search.png)

click the blue plus icon to enable the repository

![enable](/images/5-enable.png)

You will be able to see the enabled repository in the **Enabled Repositories** Column

![column](/images/6-column.png)

You will be able to see the below output after you enable all the above listed repositories

![listed](/images/7-listed.png)

## Synchronizing Content using Red Hat Satellite Dashboard

Navigate to **Content > Products** to see a list of Products. You can synchronize all repositories related to a Product or selected repositories of a product.

![products](/images/8-products.png)

Navigate to **Content > Sync Status** to check the Sync Status of all the repositories of all the products

![sync_status](/images/9-sync_status.png)

Click on **Expand All** to expand all repositories related to all products

![expand](/images/10-expand.png)

Click **Select All** to select all repositories

![select](/images/11-select.png)

Click **Synchronize Now** to synchronize content of all the repositories

![synchronize](/images/12-synchronize.png)

You will be able to see the below output once the synchronization is completed

![completed](/images/13-completes.png)

## Enabling Repository using hammer CLI

Run the following command to check all the available products and to check if any repositories are enabled for those products

```console
[ragrawal@satellite ~]$ hammer product list --organization "redhat"
```

Run the following command to check if any repositories are enabled for the product "Red Hat Enterprise Linux for x86_64"

```console
[ragrawal@satellite ~]$ hammer product list --organization "redhat" | grep "Red Hat Enterprise Linux for x86_64"
```

Run the following command to list all the available repository sets of "Red Hat Enterprise Linux for x86_64" product

```console
[ragrawal@satellite ~]$ hammer repository-set list --organization "redhat" --product "Red Hat Enterprise Linux for x86_64"
```

> [!NOTE]
> The above command lists the repository sets that are available to be enabled under a given product and organization. These are essentially groups of repositories that Red Hat provides.

Run the following command to list the individual repositories under a repository set. You will also be able to see specific release version and if the repositories are enabled.

```console
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 11049
```

Run the following command to enable the repository

```console
[ragrawal@satellite ~]$ hammer repository-set enable --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 11049 --releasever 9.5
```

Run the following command to verify the repository is enabled

```console
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 11049
```

Run the following command to list the enabled repositories for the product "Red Hat Enterprise Linux for x86_64"

```console
[ragrawal@satellite ~]$ hammer product list --organization "redhat" | grep "Red Hat Enterprise Linux for x86_64"
```

## Synchronizing Content using hammer CLI
