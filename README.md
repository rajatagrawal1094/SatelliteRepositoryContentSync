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

![completed](/images/13-completed.png)

## Enabling Repository using hammer CLI

Run the following command to list all the enabled repositories

```console
[ragrawal@satellite ~]$ hammer repository list --organization "redhat"
```

![repo_list](/images/14-repo_list.png)

Run the following command to check all the available products and to check if any repositories are enabled for those products

```console
[ragrawal@satellite ~]$ hammer product list --organization "redhat"
```

![product_list](/images/15-product_list.png)

Run the following command to check if any repositories are enabled for the product "Red Hat Enterprise Linux for x86_64"

```console
[ragrawal@satellite ~]$ hammer product list --organization "redhat" | grep "Red Hat Enterprise Linux for x86_64"
```

![rhel_list](/images/16-rhel_list.png)

Run the following command to list all the available repository sets for "Red Hat Enterprise Linux for x86_64" product

```console
[ragrawal@satellite ~]$ hammer repository-set list --organization "redhat" --product "Red Hat Enterprise Linux for x86_64"
```

![all_repo_list](/images/17-all_repo_list.png)

> [!NOTE]
> The above command lists the repository sets that are available to be enabled under a given product and organization. These are essentially groups of repositories that Red Hat provides.

Additionally, Run the following command to list all the available repository sets for "Red Hat Satellite Capsule" product

```console
[ragrawal@satellite ~]$ hammer repository-set list --organization "redhat" --product "Red Hat Satellite Capsule"
```

Run the following command to list the individual repostories under the repository sets. You will also be able to see the specific release version and if the repositories are enabled

```console
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 11049
```

![available_list](/images/18-available_list.png)

Additionally, Run the following commands to list the individual repositories under their respective repository sets.

```console
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 11055
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 7416
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 7441
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 21174
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Satellite Capsule" --id 21171
```

Run the following command to enable the repository

```console
[ragrawal@satellite ~]$ hammer repository-set enable --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 11049 --releasever 9.5
```

![enable_repo](/images/19-enable_repo.png)

Additionally, Run the following command to enable the other repositories

```console
[ragrawal@satellite ~]$ hammer repository-set enable --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 11055 --releasever 9.5
[ragrawal@satellite ~]$ hammer repository-set enable --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 7416 --releasever 8
[ragrawal@satellite ~]$ hammer repository-set enable --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 7441 --releasever 8
[ragrawal@satellite ~]$ hammer repository-set enable --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 21174
[ragrawal@satellite ~]$ hammer repository-set enable --organization "redhat" --product "Red Hat Satellite Capsule" --id 21171
```

Run the following command to verify the repository is enabled

```console
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 11049
```

![check_enabled](/images/20-check_enabled.png)

Additionally, Run the following commands to verify if all the other repositories are enabled

```console
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 11055
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 7416
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 7441
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 21174
[ragrawal@satellite ~]$ hammer repository-set available-repositories --organization "redhat" --product "Red Hat Satellite Capsule" --id 21171
```

Run the following command to list the enabled repositories for the product "Red Hat Enterprise Linux for x86_64" and "Red Hat Satellite Capsule"

```console
[ragrawal@satellite ~]$ hammer product list --organization "redhat" | grep -e "Red Hat Enterprise Linux for x86_64" -e "Red Hat Satellite Capsule"
```

![list_all_enabled](/images/21-list_all_enabled.png)

Run the following command to list all the enabled repositories

```console
[ragrawal@satellite ~]$ hammer repository list --organization "redhat"
```

![detailed_all_enabled](/images/22-detailed_all_enabled.png)

## Synchronizing Content using hammer CLI

Run the following commands to synchronize the all repositories for the product "Red Hat Enterprise Linux for x86_64"

```console
[ragrawal@satellite ~]$ hammer repository synchronize --async --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 1
[ragrawal@satellite ~]$ hammer repository synchronize --async --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 2
[ragrawal@satellite ~]$ hammer repository synchronize --async --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 3
[ragrawal@satellite ~]$ hammer repository synchronize --async --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 4
[ragrawal@satellite ~]$ hammer repository synchronize --async --organization "redhat" --product "Red Hat Enterprise Linux for x86_64" --id 5
```

![sync_all_rhel](/images/23-sync_all_rhel.png)

Run the following command to synchronize the repository for the product "Red Hat Satellite Capsule"

```console
[ragrawal@satellite ~]$ hammer repository synchronize --async --organization "redhat" --product "Red Hat Satellite Capsule" --id 6
```

![sync_sat](/images/24-sync_sat.png)

Run the following command to check the status on the repository synchronization

```console
[ragrawal@satellite ~]$ hammer product list --organization "redhat" | grep -e "Red Hat Enterprise Linux for x86_64" -e "Red Hat Satellite Capsule"
```

![check_final_status_1](/images/25-check_final_status_1.png)

![check_final_status_2](/images/26-check_final_status_2.png)

Run the following command to get the detailed information on each synchronized repository

```console                                                   
[ragrawal@satellite ~]$ hammer repository info --name "Red Hat Enterprise Linux 9 for x86_64 - BaseOS RPMs 9.5" --organization "redhat" --product "Red Hat Enterprise Linux for x86_64"
```

![check_final_details](/images/27-check_final_details.png)
