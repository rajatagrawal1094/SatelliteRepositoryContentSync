# Enabling Repository and Syncing Content to Red Hat Satellite

## Enabling Repository

Open a browser, enter the Red Hat Satellite Server URL - https://satellite.example.com

![dashboard](/images/1-dashboard.png)

Enter Credentials and click Log In button

- **Username**: admin
- **Password**: redhat

![login](/images/2-login.png)

Navigate to **Content > Red Hat Repositories**

![repositories](/images/3-repositories.png)

You will now see all available repositories. 

![available](/images/4-available.png)

We will be enabling the following:

| Name        						     | Repository 					 |
| :--------------------------------------------------------: | :-----------------------------------------------: |
| Red Hat Enterprise Linux 8 for x86_64 - AppStream RPMs 8   | rhel-8-for-x86_64-appstream-rpms             	 |
| Red Hat Enterprise Linux 8 for x86_64 - BaseOS RPMs 8      | rhel-8-for-x86_64-baseos-rpms             	 |
| Red Hat Enterprise Linux 9 for x86_64 - AppStream RPMs 9.5 | rhel-9-for-x86_64-appstream-rpms             	 |
| Red Hat Enterprise Linux 8 for x86_64 - BaseOS RPMs 9.5    | rhel-9-for-x86_64-baseos-rpms             	 |
| Red Hat Satellite Capsule 6.15 for RHEL 8 x86_64 RPMs      | satellite-capsule-6.15-for-rhel-8-x86_64-rpms     |
| Red Hat Satellite Maintenance 6.15 for RHEL 8 x86_64 RPMs  | satellite-maintenance-6.15-for-rhel-8-x86_64-rpms |

In the search bar, search for the repository names (one at a time). Click on the drop down arrow on the left side to see the available architectures.

![search](/images/5-search.png)

click blue plus icon to enable the repository.

![enable](/images/6-enable.png)

You will be able to see the below output after you enable all the above listed repositories

![listed](/images/7-listed.png)

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
