>***Disclaimer:** Links contained herein to external website(s) are provided for convenience only. Red Hat has not reviewed the links and is not responsible for the content or its availability. The inclusion of any link to an external website does not imply endorsement by Red Hat of the website or their entities, products or services. You agree that Red Hat is not responsible or liable for any loss or expenses that may result due to your use of (or reliance on) the external site or content.*

An important part of any platform used to host business and user workloads is data protection. Data protection may include operations including on-demand backup, scheduled backup and restore. These operations allow the objects within a cluster to be backed up to a storage provider, either locally or on a public cloud, and restore that cluster from the backup in the event of a failure or scheduled maintenance. 
 
Red Hat has created OpenShift API for Data Protection, or OADP, for this purpose. OADP brings an API to the OpenShift Container Platform that Red Hat partners can leverage in creating a disaster recovery and data protection solution. 

## Frequently Asked Questions

### **What is OADP?**
OADP (OpenShift APIs for Data Protection) is an operator that Red Hat has created to create backup and restore APIs in the OpenShift cluster.
You can read more about OADP in the following links: 
[OADP documentation](https://docs.openshift.com/container-platform/latest/backup_and_restore/application_backup_and_restore/oadp-intro.html)
[OADP Customer Portal: verified solutions, articles, and discussions with support](https://access.redhat.com/search/?q=OADP&p=1&rows=10&documentKind=Solution%26Article%26Discussion&sort=lastModifiedDate+desc)
[Getting Started with OADP and OpenShift Virtualization](https://developers.redhat.com/articles/2024/08/21/how-back-and-restore-virtual-machines-openshift)
[OADP blog posts](https://cloud.redhat.com/blog/search-results?term=oadp)
[Red Hat Experts a.k.a MOB, OADP Blogs](https://cloud.redhat.com/experts/aro/backup-restore/)
[OADP Troubleshooting Guide](https://github.com/openshift/oadp-operator/blob/master/docs/TROUBLESHOOTING.md)
[Backup OpenShift applications using the OpenShift API for Data Protection with Multicloud Object Gateway](https://cloud.redhat.com/blog/backup-openshift-applications-using-the-openshift-api-for-data-protection-with-multicloud-object-gateway)
[Red Hat OADP Training](https://role.rhu.redhat.com/rol-rhu/app/courses/do380-4.14/pages/ch02s03)
[Velero Documentation - latest](https://velero.io/docs/main/)
[Velero Code Wiki](https://codewiki.google/github.com/vmware-tanzu/velero)

### **Currently Supported Versions of OADP**
- [Official OpenShift Operator Life Cycle Support Page](https://access.redhat.com/support/policy/updates/openshift_operators)
  - Search for "API for Data Protection"
- [Product Life Cycles](https://access.redhat.com/product-life-cycles?product=OpenShift%20APIs%20for%20Data%20Protection)
- OADP-1.3 on OCP 4.12 - 4.15
- OADP-1.4 on OCP 4.14 - 4.18
- OADP-1.5 on OCP 4.19 - 4.21
- OADP-1.6 on OCP 4.22 - 4.23
- OADP-1.6 on OCP 5.0 - OCP 5.1

### **Future Versions of OADP**
Customers and partners should refer to our [Partners page](https://github.com/openshift/oadp-operator/blob/master/PARTNERS.md) to better understand future supported versions on OADP.

### **OADP-1.6**
*  PVC's using storage class with bindingMode waitForFirstConsumer ( not Immediate ) may fail to bind to PV when node affiinity is configured. This may occur in other situations based on the clusters configuration.

  * **Solution:** Configured the DPA nodeagent to ignore binding delays with:
~~~
spec:
  backupLocations:
  - velero:
      config:
        profile: default
        region: us-west-2
      credential:
        key: cloud
        name: cloud-credentials
      default: true
      objectStorage:
        bucket: bucket
        prefix: mine
      provider: aws
  configuration:
    nodeAgent:
      enable: true
      restorePVC:
        ignoreDelayBinding: true    # <------------
      uploaderType: kopia
~~~

### **AWS S3 compatible backup storage providers**
- [Supported S3 Object storage](https://docs.redhat.com/en/documentation/openshift_container_platform/latest/html/backup_and_restore/oadp-application-backup-and-restore#oadp-s3-compatible-backup-storage-providers-supported)

-  Variations with S3 providers and the AWS SDKV1 and SDKV2 can cause problems for some customers.  The latest OADP-1.4 releases provides both the `aws` and now `legacy-aws` plugin options. See our [documentation for details](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/backup_and_restore/oadp-application-backup-and-restore#oadp-using-legacy-aws-plugin)

- Known issues with S3 providers
  - [Velero documentation](https://github.com/vmware-tanzu/velero/issues/8265#issue-2567228797)
  - [OpenShift documentation](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/installing/about-installing-oadp.html#oadp-s3-compatible-backup-storage-providers-known-limitations)


### **S3 object locks and versioning**
- OADP does not support S3 configurations for backup data immutability across many S3 providers, see our [documentation for details](https://docs.redhat.com/en/documentation/openshift_container_platform/latest/html/backup_and_restore/oadp-application-backup-and-restore#oadp-support-backup-data-immutability_about-installing-oadp)
 - S3 object lock
 - Object retention
 - Bucket versioning
 - Write Once Read Many (WORM) buckets

**Note** this is an area where we are testing various s3 providers and their various types of support for locking and for versioning.  Expect future updates to the OADP documentation.



### **How to upgrade OADP**
Please reference the official documentation for OADP upgrades.

- [Upgrade from OADP-1.1 to OADP-1.2](https://docs.openshift.com/container-platform/latest/backup_and_restore/application_backup_and_restore/release-notes/oadp-release-notes-1-2.html#Upgrade-notes-1-2-0_oadp-release-notes)
- [Upgrade from OADP-1.2 to OADP-1.3](https://docs.openshift.com/container-platform/latest/backup_and_restore/application_backup_and_restore/release-notes/oadp-release-notes-1-3.html#upgrade-notes-1-3-0_oadp-release-notes)
- [Upgrade from OADP-1.3 to OADP-1.4](https://docs.openshift.com/container-platform/4.16/backup_and_restore/application_backup_and_restore/release-notes/oadp-1-4-release-notes.html#upgrade-notes-1-4-0_oadp-1-4-release-notes)
- [Upgrade from OADP-1.4 to OADP-1.5](https://docs.redhat.com/en/documentation/openshift_container_platform/4.19/html/backup_and_restore/oadp-application-backup-and-restore#upgrade-notes-1-5-0_oadp-1-5-release-notes)

### **Debugging OADP, oadp-must-gather**
- [OADP's must-gather documentation](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/troubleshooting/using-the-must-gather-tool.html)
- NOTE: run w/ --skip-tls
~~~
OADP-1.5: oc adm must-gather --image=registry.redhat.io/oadp/oadp-mustgather-rhel9:v1.5 -- /usr/bin/gather --skip-tls
OADP-1.4: oc adm must-gather --image=registry.redhat.io/oadp/oadp-mustgather-rhel9:v1.4 -- /usr/bin/gather --skip-tls
OADP-1.3: oc adm must-gather --image=registry.redhat.io/oadp/oadp-mustgather-rhel9:v1.3 -- /usr/bin/gather --skip-tls
~~~
- [Debugging tips from the engineering team](https://github.com/openshift/oadp-operator/blob/master/docs/TROUBLESHOOTING.md)

### **How can I check the details for each container OADP deploys**

One can find details on all the containers Red Hat ships for [OpenShift in the Red Hat Container Catalog](https://catalog.redhat.com/search?searchType=containers&product_listings_names=OpenShift%20API%20for%20Data%20Protection&p=1&partnerName=Red%20Hat&release_categories=Generally%20Available)

The above link will filter for OADP.  Please note that releases  >= OADP 1.3.0 are built on the rhel9 UBI container image, for example 'oadp/oadp-velero-plugin-for-csi-rhel9'
Here you will find: 
- Security information
- Git and source related information
- RPM packages

### **Need a UI with OADP?**
Please checkout our partnership and collaboration with [CloudCasa!](https://cloudcasa.io/)  CloudCasa can provide a hosted or on-premise web based user interface that integrates with OADP.  For details please refer to our [partner page](https://cloudcasa.io/partners/red-hat-openshift/)

### **What APIs does the operator provide?**
OADP provides the following APIs:

- Backup 
- Restore 
- Schedule 
- BackupStorageLocation 
- VolumeSnapshotLocation

Red Hat has **not** added, removed or modified any of the APIs as documented in the Velero upstream project. The Velero site has more details on the [Velero API Types](https://velero.io/docs/main/api-types/).

### **Can OADP backup my entire cluster?**
No.  OADP is meant to backup customer applications on the OpenShift Platform.  OADP will not successfully backup and restore operators or etcd.  There are a variety of ways to customize a backup to avoid backing up inappropriate resources via namespaces or labels.  

### **Is there an upstream project for OADP?**
Yes. The OADP operator is developed in the [oadp-operator](https://github.com/openshift/oadp-operator) upstream project.

### **What is the support status of the OADP operator?**
Please refer to the [OADP support policy](https://access.redhat.com/support/policy/updates/openshift#oadp)

### **Is OADP a full end-to-end data protection solution?**
OpenShift API for Data Protection (OADP) features provide options for backing up and restoring applications. You can find more detail regarding OADP's features in our [documentation](https://docs.openshift.com/container-platform/latest/backup_and_restore/application_backup_and_restore/oadp-features-plugins.html)

### **What data can OADP protect?**
OADP provides APIs to backup and restore OpenShift cluster resources (yaml files), internal images and persistent volume  data.

### **What is the OADP operator installing?**
The OADP operator will install Velero, and OpenShift plugins for Velero to use, for backup and restore operations.

### **Can I install multiple versions of OADP in the same cluster?**
No, each OADP version can have different CustomResourceDefinitions. Only *one version* of OADP will work properly if *multiple OADP versions* are installed in the same cluster.
It is recommended to have a single version of OADP (and Velero) installed in the cluster. Refer to [OADP and Velero Version relationship](https://github.com/openshift/oadp-operator#velero-version-relationship)

### **Known issues with cloud providers and hyperscalers**
- IBMCloud:
  - IBMCloud's  k8s hostpath by default is set to /var/data/kublet/pods [see the following issue for details](https://github.com/vmware-tanzu/velero/pull/8069)
    - The issue will cause OADP's node-agents to crash.
    - OADP will automatically detect the OpenShift cluster is running on IBMCloud and make the adjustment. (See the following details)[https://issues.redhat.com/browse/OADP-4623]
    - To override the hostpath settings please review and update OADP csv settings.
~~~
oc get csv oadp-operator.v1.4.1 -o yaml
oc get nodes
oc debug node/$node
~~~
- Verify the path to $path/kublet/pods and $path/kublet/plugins
- Adjust the settings in the CSV as needed.
~~~
containers:
- args:
  - --leader-elect
  command:
  - /manager
  env:
  - name: WATCH_NAMESPACE
    valueFrom:
      fieldRef:
        fieldPath: metadata.annotations['olm.targetNamespaces']
  - name: RESTIC_PV_HOSTPATH
  - name: FS_PV_HOSTPATH
    value: /var/lib/kubelet/pods
  - name: PLUGINS_HOSTPATH
    value: /var/lib/kubelet/plugins
~~~
- Huawei:
  - It has been reported that Huawei has similar issues to IBMCloud's hostpath settings.  The same type of customizations may be required for the node-agents to work properly.

### **Can I install OADP alongside MTC?**
As long as the OADP version you install is the same version as the OADP version depended on by MTC, it can be done.
You cannot install MTC 1.7 which expects OADP 1.0, as well as install OADP 1.1 for example. You can only install OADP 1.0 in this scenario.

### **Does OADP support CSI snapshots?**
Yes, please refer to the [documentation](https://docs.openshift.com/container-platform/4.11/backup_and_restore/application_backup_and_restore/installing/installing-oadp-ocs.html)

### **Virtual Machine (VM) Backups fail on virt-freeze**
* virt-freeze issues are fixed in OADP-1.6 and OADP-1.5.  
* OCP 4.18 - fix in progress https://redhat.atlassian.net/browse/CNV-91071 
Typically on Windows VM's the virt-freeze command can intermittently fail.  Retrying is currently the only known workaround.
See issues: 
  * [CNV-75370](https://issues.redhat.com/browse/CNV-75370)
  *  [CNV-79727](https://redhat.atlassian.net/browse/CNV-79727)
  * [CNV-56743](https://issues.redhat.com/browse/CNV-56743)

FSFreeze fails with permission denied: 
  * [ jira issue](https://redhat.atlassian.net/browse/CNV-32664) 
  * [ bugzilla ](https://bugzilla.redhat.com/show_bug.cgi?id=2237678)

Removing Kubevirt Freeze Hooks:
  * KCS: [OpenShift Virtualization: OADP or Cohesity backup freezes VM during backup ](https://access.redhat.com/solutions/7137659)

[Overview of Processing a Backup Under VSS](https://learn.microsoft.com/en-us/windows/win32/vss/overview-of-processing-a-backup-under-vss)
  * Unofficial and unsupported workaround: [here](https://github.com/weshayutin/kubevirt-velero-annotations-remover)
  * Unofficial and unsupported ACM policy: [here](https://github.com/mhenriks/kubevirt-strip-velero-hooks)

For freeze issues related to vss polling timing out in [windows vss](https://learn.microsoft.com/en-us/windows/win32/vss/overview-of-processing-a-backup-under-vss)
Call Red Hat support to get a support exception for using the following OADP overrides.  An official fix will be released soon.

oadp-1.5 - Unreleased FIX:  [OADP-7883](https://redhat.atlassian.net/browse/OADP-7883)
Current Workaround:
~~~
unsupportedOverrides:
   veleroImageFqin: quay.io/sseago/velero:csi-quick-poll
~~~
oadp-1.4 - Unreleased FIX: [OADP-7884](https://redhat.atlassian.net/browse/OADP-7884)
Current Workaround:
~~~
unsupportedOverrides:
  veleroImageFqin: quay.io/spampatt/velero:csi-polling
~~~

Upstream fix for Velero
* [Fix for Velero 1.18]( https://github.com/vmware-tanzu/velero/pull/9629)  This fix will be backported to OADP-1.4, and OADP-1.5
* [Fix for future versions](https://github.com/vmware-tanzu/velero/pull/9602)

### **Are there plans to include a data mover with OADP?**
The data mover is fully supported in OADP 1.3.0 and above

### **Can users create their own backups? Stated another way, can non cluster admin users create backup and restores?** 
Yes, as of OADP-1.5.0 OADP supports self-service support for our customers. [Self Service Documentation](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/oadp-self-service/oadp-self-service.html)

### **Velero backup [logs,describe] commands error w/ "tls: failed to verify certificate: x509"**
Access the velero command using these instructions:  [Doc](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/troubleshooting/velero-cli-tool.html#velero-obtaining-by-accessing-binary_velero-cli-tool)
The DPA certificate settings do not change the behavior of the velero cli when executed from a client machine.  Check the --help on the `velero backup logs` command.
~~~
Usage:
  velero backup logs BACKUP [flags]

Flags:
      --cacert string              Path to a certificate bundle to use when verifying TLS connections.
  -h, --help                       help for logs
      --insecure-skip-tls-verify   If true, the object store's TLS certificate will not be checked for validity. This is insecure and susceptible to man-in-the-middle attacks. Not recommended for production.

The --cacert and --insecure-skip-tls-verify flags should ONLY be used with the following velero commands.
* velero backup describe
* velero backup download
* velero backup logs
* velero restore describe
* velero restore logs
~~~ 

If you want to use cacert with this command, you can add cert to the velero deployment like so
~~~
$ oc get dataprotectionapplications.oadp.openshift.io <dpa-name> -o jsonpath='{.spec.backupLocations[0].velero.objectStorage.caCert}' | base64 -d | oc exec -i deploy/velero -c velero -- bash -c "cat > /tmp/your-cacert.txt"
~~~

### **How do I determine the version of Velero OADP installed?**
After OADP installation, the **velero** deployment it will contain the tag of the image. If you install OADP with the default config you will be using upstream tagged images with the version called out in the deployment. You can also check out the [version matrix](https://github.com/openshift/oadp-operator#version).

### **Where can I find examples of using OADP APIs for backup/restore?**
The OADP operator page in the upstream oadp-operator project  has [examples](https://github.com/openshift/oadp-operator/tree/master/docs/examples) that walk through usage.  We also maintain [sample applications](https://github.com/openshift/oadp-operator/tree/master/tests/e2e/sample-applications) 

### **Using S3 compatible storage that does not have an associated region**
There are S3 compatible storage implementations that do not require a region to be setup.  In these cases simply substitute a valid aws region like "us-east-1" in the DPA yaml configuration.  For example the [OADP with MCG](https://docs.openshift.com/container-platform/4.11/backup_and_restore/application_backup_and_restore/installing/installing-oadp-mcg.html) documentation.   Reference the velero [issue](https://github.com/vmware-tanzu/velero/issues/4305)

- A user should provide the:
    - s3Url: https://foo/storage
    - region: us-east-1

~~~
 backupLocations:
    - velero:
        config:
          profile: "default"
          region: us-east-1
          s3Url:  https://foo/storage <s3 endpoint>
          insecureSkipTLSVerify: "true"
          s3ForcePathStyle: "true"
        provider: aws
        default: true
        credential:
          key: cloud
          name: cloud-credentials 
        objectStorage:
          bucket: <bucket_name> 
          prefix: <prefix> 
~~~ 

### **Working with Kopia repositories**
* A user can use the kopia client to attach to backup repositories in s3.
~~~
export S3_BUCKET=<your bucket name>
export S3_REPOSITORY_PATH=<path without S3_BUCKET>
export S3_ACCESS_KEY=<s3 access key>
export S3_SECRET_ACCESS_KEY=<s3 secret access key>

"static-passw0rd" is the default password

kopia repository connect s3 \
    --bucket="$S3_BUCKET" \
    --prefix="$S3_REPOSITORY_PATH" \
    --access-key="$S3_ACCESS_KEY" \
    --secret-access-key="$S3_SECRET_ACCESS_KEY" \
    --password=static-passw0rd
~~~ 

kopia client: https://kopia.io/docs/reference/command-line/
kopia common commands: https://kopia.io/docs/reference/command-line/common/
kopia advanced commands: https://kopia.io/docs/reference/command-line/advanced/

### **Incremental Backup**
At the moment visualizing the savings from OADP incremental backups is not obvious. Improvements are being made in this regard.
One can find examples on how to determine the exact details of each incremental backup via the following link:
  * [kopia troubleshooting](https://github.com/openshift/oadp-operator/blob/oadp-dev/docs/kopia_troubleshooting.md#basic-commands)

Note: the new-data, new-files keys from the output below.
~~~
2025-09-26 15:35:53 UTC kc492e2ac155921724d6c61c8f4be240b 108.3 MB dgrwxrwxr-x files:101 dirs:6 new-data:15.9 MB new-files:83 new-dirs:6 compression:0.0% (latest-2) pins:velero-pin
2025-09-26 15:38:04 UTC k8d3195f8fb0c0ee9ccc45f4a2be4f34e 108.3 MB dgrwxrwxr-x files:104 dirs:6 new-data:68 B new-files:1 new-dirs:1 compression:0% latest-1,hourly-1,daily-1,weekly-1,monthly-1,annual-1) pins:velero-pin
~~~


### **Can OADP restore routes with base domain from the restore cluster?**
OADP will restore routes with base domain from the restore cluster when the route being restored is a generated route

A generated route is a route that do not specify route.spec.host at creation and let OpenShift generates the hostname for the route. Generated route will have annotation "openshift.io/host.generated: 'true'". If you manually add this annotation to a route then unexpected behavior may occur during restore. If the user have modified the host value from a generated value, the host value can be lost on restore.

There is no mechanism at this time in OADP to dynamically set route host value based on cluster base domain name for a non generated route.

Likewise, for a generated route, the host value will be stripped by oadp-operator to be regenerated on restore cluster. Any modifications to .spec.host of a generated route will be lost on restore.


### **Can I turn off internal registry image backup?**
If you experienced issues during backup or restore due to errors related to internal registry image (imagestreams) backup you can turn off image backup functionality like so in the DataProtectionApplication spec.
~~~ 
spec:
  backupImages: false // set this to disable image backup/restore
~~~ 

### **Set a backup to expire**
When you create a backup, you can specify a TTL (time to live) by adding the flag --ttl <DURATION>. If Velero sees that an existing backup resource is expired, it removes:

* The backup resource
* The backup file from cloud object storage
* All PersistentVolume snapshots
* All associated Restores

[Upstream Documentation with Details](https://velero.io/docs/v1.14/how-velero-works/#set-a-backup-to-expire)

### **Issues restoring an OADP backup: application unable to access data**
When a Namespace is created in OpenShift, it is assigned a unique User Id (UID) range, a Supplemental Group (GID) range, and unique SELinux MCS labels. This information is stored in the metadata.annotations field of the Namespace. Every time a new Namespace is created, OpenShift assigns it a new range from its available pool of UIDs and updates the metadata.annotations field to reflect the assigned values. We will refer to these annotations as SCC (SecurityContextConstaints) annotations.

However, if the Namespace resource already has those annotations set, OpenShift does not re-assign new values for the Namespace. It instead assumes that the existing values are valid and moves on.

These are the SCC annotations on OpenShift namespaces
* openshift.io/sa.scc.mcs
* openshift.io/sa.scc.supplemental-groups
* openshift.io/sa.scc.uid-range

Workload may not have data access after restore if
* there is a pre-existing namespace with a different SCC annotations than at backup time, such as on a different cluster, OADP will reuse pre-existing namespace.
* backup used a label selector and the namespace where workloads runs on doesn't have the label on it. OADP will not backup the namespace but will create a new namespace without previous namespace annotations during restore causing a new UID range to be assigned to the namespace.

This can be an issue for customer workloads as OpenShift assigns a pod securityContext UID based on namespace annotations which in this case has changed from the time the persistent volume data was backup.
* container UID no longer matches the file owner's UID
* application can complain that it cannot read/write to data owned by a different UID

Simple mitigations include
* Adding label selector to namespace containing workload when using label selector to filter objects to include in backup.
* Removing pre-existing namespace before restoring

Advanced mitigations
* Updating owners of files in the restored cluster by following [Fixing UID ranges after migration](https://access.redhat.com/articles/6844071#:~:text=Fixing%20UID%20ranges%20after%20migration) with step 2-4

There are risks associated with restoring namespace in a new cluster from backup including potential for UID range collisions with another namespace. To mitigate these risks, customer can optionally follow [Fixing UID ranges after migration](https://access.redhat.com/articles/6844071#:~:text=Fixing%20UID%20ranges%20after%20migration) with step 1-4

For more information on OpenShift's UID/GID range (reference [A Guide to OpenShift and UIDs](https://cloud.redhat.com/blog/a-guide-to-openshift-and-uids))


### **Backing up data from one cluster and restoring to another cluster**
- To successfully backup and restore data to two different clusters please ensure that in your DPA config on both clusters that:
  - [OpenShift Documentation](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/oadp-advanced-topics.html#backing-up-data-one-cluster-restoring-another-cluster)
  - The backup store location (BSL) and volume snapshot location have the same names and paths to restore resources to another cluster.
  -  The same object storage location credentials must be shared across the clusters
  -  The upstream Velero [documentation](https://velero.io/docs/main/migration-case/) is helpful in the case. 
  -  For Volume backup and restore please refer to the latest OADP documentation and the datamover sections.
  -  Allow OADP to create the namespace on the destination cluster for best results.
  - When restoring PVCs into a namespace where the volumes already exist, prior to restore you should first delete any PVCs that need to be updated. For Restic use cases, the Deployment (or DC, etc.) for the mounting pod must also be removed, assuming that the Deployment is also in the backup being restored.


## **Disaster recovery - Using Schedules and Read-Only Backup Storage Locations**
During disaster recovery, it is recommended that you set your backup location accessMode to `ReadOnly` to prevent addition/deletions to the backup storage location during the restore process.

You would set accessMode to readOnly like so in the DataProtectionApplication spec
~~~
...
spec:
  backupLocations:
    - velero:
        accessMode: ReadOnly
...
~~~
Proceed to restore from backup.

### **OADP Restore fails with ArgoCD**
If ArgoCD is being used during a restore, it is possible to see the restore fail. This could be caused by a label used by ArgoCD `app.kubernetes.io/instance`. This label is used to identify which resources ArgoCD needs to manage, which can create conflict with OADP managing resources on restore. 

To resolve this issue, you can set `.spec.resourceTrackingMethod` on the ArgoCD yaml to `annotation+label` or `annotation`.  If issues still persist, then disable ArgoCD before restore, and then enable again once restore completes.

Related work:
- [Add Backup warning for inclusion of NS managed by ArgoCD](https://github.com/vmware-tanzu/velero/pull/8257)
- [Volumesnapshot getting deleted during backup (argocd)](https://github.com/vmware-tanzu/velero/issues/7905)
- [OADP + OpenShift GitOps - An approach to implementing application disaster recovery](https://www.redhat.com/en/blog/oadp-openshift-gitops-an-approach-to-implementing-application-disaster-recovery)

Please do [let us know](https://access.redhat.com/support/cases/#/case/new/open-case/describe-issue?caseCreate=true&product=OpenShift%20API%20for%20Data%20Protection&version=) when the errors occur so we work to resolve the issue.

### **Can I install OADP into multiple OpenShift Projects to enable project owners?**
We will be providing additional documentation to cover this usecase in the near future. We are actively working on this usecase over at [github.com/migtools/oadp-non-admin](https://github.com/migtools/oadp-non-admin) tracked in [OADP-3931](https://issues.redhat.com/browse/OADP-3931), however it is worth noting here.  It is possible to install OADP into multiple namespaces to enable multiple cluster admins to manage their own OADP instance.   The deployments of OADP must all be at the same version, installing different versions of OADP on the same cluster is NOT supported.   

- It is required that each individual deployment of OADP have a unique set of credentials and BackupStorageLocation configuration.  The workflow has been validated with Restic and CSI.
- It is worth noting that by default each OADP deployment has cluster level access across namespaces.

### **I am trying to use OADP with a ROSA cluster, and need help**
We have recently updated the documentation for installing and configuring OADP with ROSA clusters.  Please see the documentation [here](https://docs.openshift.com/rosa/rosa_backing_up_and_restoring_applications/backing-up-applications.html)

### **I set a very short TTL for backup, but the data still exists after TTL expires **
The effects of expiration are not applied immediately, they are applied when the gc-controller runs its reconciliation loop every hour.

### **OADP-1.2.x Datamover enabled backup/restore is stuck in  WaitingForPluginOperations **
* One potential cause of the backup being stuck in wait are restic locks.   To determine if the root cause are restic locks, cycle through the vsb with the following command.
~~~
 oc get vsb -n <protected-ns> -o yaml | grep resticrepository
~~~
* Look for an error referencing the restic lock, `Fatal: unable to create lock in backend: repository is already locked`
* The lock must be removed for the backup/restore to be successful.
* Please reference:
  * https://restic.readthedocs.io/en/stable/100_references.html?highlight=lock#locks
  * https://forum.restic.net/t/detecting-stale-locks/1889/15
  * https://github.com/restic/restic/issues/1450

### ** Note: Datamover backups in OADP 1.1 requires vsb cleanup when run via a schedule or repetitively **

If you are running velero backups via the velero scheduler with datamover enabled, vsb's need to removed to avoid inconsistent content in the velero restore.  This also applies to repetitive backups executed manually or programmatically.  Please see vsb cleanup instructions in this document.
 
A fix for this issue will NOT be released for OADP 1.1.x.  Customers will need to upgrade to OADP 1.2.x for the fix.

To avoid issues with the velero scheduler we recommend executing the velero backup via a [k8s cron job](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/) that include the backup command and the vsb cleanup.

### **Datamover backup cleanup for OADP 1.1 **
In OADP 1.1, some resources can be left behind by datamover.

**Remove snapshots in bucket**

There will be snapshots in your bucket specified in the DPA `.spec.backupLocation.objectStorage.bucket` under `/<protected-ns>`
  - delete this folder to delete **all** snapshots in your bucket.

In the `/<protected-ns>` folder, there will be additional folder(s) prefixed with `/<volumeSnapshotContent name>-pvc` where volumeSnapshotContent name is the volumeSnapshotContent created by datamover per PVC.
  - delete this folder to delete **a single** snapshot in your bucket.

**Remove cluster resources:** There are two main scenarios:

**1. Datamover completes: volumeSnapshotBackup/volumeSnapshotRestore CRs still exist in the application namespace.**

  Datamover backup:
  `oc delete vsb -n <app-ns> --all`

  Datamover restore:
  `oc delete vsr -n <app-ns> --all`

 - Note: There will also be volumeSnapshotContents that can be deleted if needed
  `oc delete volumesnapshotcontent --all`

**2. Datamover partiallyFails or Fails: VSB/VSR CRs exist in the application namespace, as well as extra resources created by these controllers.**

  Datamover backup:

   `oc delete vsb -n <app-ns> --all`

   `oc delete volumesnapshot -A --all`

   `oc delete volumesnapshotcontent --all`

   `oc delete pvc -n <protected-ns> --all`

   `oc delete replicationsource -n <protected-ns> --all`

  Datamover restore:

   `oc delete vsr -n <app-ns> --all`

   `oc delete volumesnapshot -A --all`

   `oc delete volumesnapshotcontent --all`

   `oc delete replicationdestination -n <protected-ns> --all`

### **Failed to check and update snapshot content in a VolumeSnapshotContent Object**
Users may notice that during a backup that a VolumeSnapShotContent object will be created per Volume.  Users may also notice the VolumeSnapShotContents object in an error state similar to the following.   This is a known transient issue and should resolve as OpenShift reconciles the VSC's.  For more details see: [Get error when creating volume snapshot](https://github.com/kubernetes-csi/external-snapshotter/issues/300)
~~~
      Failed to check and update snapshot content: failed to remove
      VolumeSnapshotBeingCreated annotation on the content
      snapcontent-6cd696d3-2cf4-4c4d-8d96-439dc090b10b: "snapshot controller
      failed to update snapcontent-6cd696d3-2cf4-4c4d-8d96-439dc090b10b on API
      server: Operation cannot be fulfilled on
      volumesnapshotcontents.snapshot.storage.k8s.io
      \"snapcontent-6cd696d3-2cf4-4c4d-8d96-439dc090b10b\": the object has been
      modified; please apply your changes to the latest version and try again"
~~~

### **How does OADP's data mover for CSI snapshots work?**
We have a nice [blog post](https://cloud.redhat.com/blog/an-overview-of-data-mover) describing in detail how OADP datamover works.  Also see our [public documentation](https://docs.openshift.com/container-platform/4.12/backup_and_restore/application_backup_and_restore/backing_up_and_restoring/backing-up-applications.html#oadp-using-data-mover-for-csi-snapshots_backing-up-applications)

### **VolumeSnapContent in failed state**

You may find the following error causing backups to take longer than usual or to ultimately fail:
~~~
snapshot controller failed to update or failed to remove...xxxxx
the object has been modified; please apply your changes to the latest version and try again
~~~
- This is a [known issue](https://github.com/kubernetes-csi/external-snapshotter/issues/748) and a fix is available.
- It may be possible to delete the failed volume snapshot contents object, it should automatically be recreated.  Please ensure your backup can be restored successfully with the correct data in such cases.

### **Backup partially falling for BuildConfig application**

Backup may partially fail when build pods are part of the backup due to build pods being completed.

Workaround is to exclude volumes from being included in the backup of build pods by adding the following annotation to build pods `backup.velero.io/backup-volumes-excludes=buildworkdir,container-storage-root,build-blob-cache`

Build pods can be identified by label or annotation `openshift.io/build.name=somebuildname`

Command to annotate build pods 
~~~
NS=<backup-includedNamespace> && oc annotate -n $NS $(oc get pods -n $NS -oname -l openshift.io/build.name=<buildName>) backup.velero.io/backup-volumes-excludes=buildworkdir,container-storage-root,container-storage-run,build-blob-cache
~~~

### **Is it possible to backup  3scale API Mgmt with OADP**
Please refer to this [article](https://access.redhat.com/solutions/7000077)

### **Source file not found, at least one source file could not be read**
- When using filesystem level volume backups (FSB), you observe something similar in the backup
logs as shown below
~~~
time="2023-09-06T06:04:37Z" level=error msg="Error backing up item" backup=openshift-adp/schedule-202309045804985 error="pod volume backup failed: running Restic backup, stderr={\"message_type\":\"error\",\"error\":{\"Op\":\"lstat\",\"Path\":\"application-name-77d8987g765v-76vqv_2023-08-09-22-04.log\",\"Err\":2},\"during\":\"archival\",\"item\":\"/host_pods/3dfghjkytdcvb-rfbijn-47b85-ftrv3i-34567ng4i/volumes/kubernetes.io~azure-file/pvc-45678-dfgjy6-dfjg6vft-7657fv654c/application-name-77d89cf56c-76vqv_2023-08-09-22-04.log\"}
~~~
- or
~~~
\"error\":{\"Op\":\"lstat\",\"Path\":\"indices/IF-3KSDFGHG3-
Zy/0/index/_2x79j_1_Lucene91_1.dvm\",\"Err\":2},\"during\":\"archival\",\"item\":\"/
host_pods/41ce-a170-28casfdafdg/volumes/kubernetes.io~csi/
pvc-4a8ba939-8bd0-443b-91aa-cb0a36066586/mount/indices/IF-3K2QkQLSG3-ZyKKa1Nw/0/index/
_2x79j_1_Lucene91_1.dvm\"}\nWarning: at least one source file could not be read\n: error
running restic
~~~
This happens when there is churn in the filesystem and the file is no longer present while performing pod volume backup. It is likely that the file was present during restic's initial scan of the volume but was removed at the point when the file was actually backed up to the restic store.
- Consider using a CSI backup
- Consider excluding the volume


### **error validating existing CRs against new CRD''s schema for "podvolumerestores.velero.io"**
If you have an installplan error upon upgrading to OADP 1.2+ from prior versions, it means you have created a restore prior to upgrading.

During velero restore when restic is enabled, a podvolumerestore custom resource is created when restoring persistent volume data.

In OADP 1.2, the podvolumerestores object have a new required field that OADP 1.1 podvolumerestore objects won't have. As long as the podvolumerestores are not in-progress they are safe to remove, as new ones will be regenerated when another restore is created.

Delete all podvolumerestores to proceed with the upgrade.

### **Using cacert with velero command aliased via velero deployment**

Some users may want to use velero CLI without installing it locally on their system.

They can do so using aliased velero command like so
~~~
alias velero='oc -n openshift-adp exec deployment/velero -c velero -it -- ./velero'
~~~

If you want to use cacert with this command, you can add cert to the velero deployment like so
~~~
$ oc get dataprotectionapplications.oadp.openshift.io <dpa-name> -o jsonpath='{.spec.backupLocations[0].velero.objectStorage.caCert}' | base64 -d | oc exec -i deploy/velero -c velero -- bash -c "cat > /tmp/your-cacert.txt"
~~~

~~~
velero describe backup <backup-name> --details --cacert /tmp/your-cacert.txt
~~~

In future versions of OADP, we may mount the cert to the velero pod for your convenience to eliminate the extra step above.

### **Backups failing with s3 compatible (MCG/ODF/IBM) BackupStorageLocation(BSL) when checksumAlgorithm is not set in BSL config**
While performing a backup of any application with Noobaa as the backup location, if the `checksumAlgorithm` configuration parameter is not set, backup fails. To work around this problem, an empty value of `checksumAlgorithm` is added to the Backup Storage Location (BSL) configuration if you have not provided this value.
The empty value is only added for BSLs that are created using Data Protection Application (DPA) custom resource (CR), and this value is not added if BSLs are created using any other method. This is applicable for OADP 1.4+.

### **Azure Files CSI Driver and Restores**
AzureFile CSI driver supports only takings snapshots, but no restoring.  To work around this issue the OADP recommends reviewing:
- [CloudCasa](https://cloudcasa.io/blog/automating-azure-files-restore-in-aks/) CloudCasa integrates with OADP or stock Velero.
- [Red Hat knowledge base article](https://access.redhat.com/solutions/7011280)
 
### **Configure NodeAgents and Node Labels**
OADP's DPA use the k8s nodeSelector to pick which nodes can run the nodeAgent.  Any label specified must match the labels on EACH node.
- The below example is an anti-pattern and will not work unless both labels are on the node.
~~~
 28   configuration:
 29     nodeAgent:
 30       enable: true
 31       podConfig:
 32         nodeSelector:
 33           'node-role.kubernetes.io/infra: ""'
 34           'node-role.kubernetes.io/worker: ""'
~~~
- The correct way to run the nodeAgent on any node you choose would be to label the nodes with a custom label 
  - 'node-role.kubernetes.io/nodeAgent: ""
~~~
 28   configuration:
 29     nodeAgent:
 30       enable: true
 31       podConfig:
 32         nodeSelector:
 33           'node-role.kubernetes.io/nodeAgent: ""'

~~~

### **Backing up and Restoring Windows Virtual Machines**
Known Issues: 
- [OADP backup of Windows VMs ends with PartiallyFailed status due to guest-agent](https://access.redhat.com/solutions/7101204)

### **Virtual Hosted Style buckets do not work with File System Backup**
Known issue: https://github.com/vmware-tanzu/velero/issues/8739
Impacts Tencent Cloud Object Storage (Tencent COS)

### How to backup only the pv/pvc data, and not the related pod
- The following is an example of only backing up pv/pvc data via CSI snapshots
~~~
apiVersion: velero.io/v1
kind: Backup
metadata:
  # A name for your backup
  name: my-pvc-only-backup
  # The namespace where OADP/Velero is installed
  namespace: openshift-adp
spec:
  # A list of namespaces to include in the backup.
  includedNamespaces:
  - ecm-adt02

  # A list of resource types to include in the backup.
  # Only these resources will be backed up from the included namespaces.
  includedResources:
  - persistentvolumeclaims

  # The name of the backup storage location where this backup should be stored.
  storageLocation: ecm

  # The amount of time before this backup is considered expired and eligible
  # for garbage collection.
  ttl: 720h0m0s
~~~
Note: 
- You need Velero installed with csi plugin, please ensure that this is the case: https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/backup_and_restore/oadp-application-backup-and-restore#oadp-enabling-csi-dpa_installing-oadp-aws 
- You need to full fill all the pre-requisites for csi snapshots backup: https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/backup_and_restore/oadp-application-backup-and-restore#oadp-backing-up-pvs-csi-doc

### **SELinux relabelling in Openshift Data Foundation / Openshift Container Storage **
- [Configuring backup and restore PVCs for Data Mover](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/installing/configuring-backup-restore-pvc-datamover.html)
- [Workarounds to skip SELinux relabelling in Openshift Data Foundation / Openshift Container Storage](https://access.redhat.com/solutions/6906261)

### **Ceph capacity is higher than expected after restoring VM's**
- [See the documentation](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/installing/installing-oadp-kubevirt.html#oadp-restore-single-vm_installing-oadp-kubevirt)

### **Configuring CephFS PVCs for Data Mover**
- [See the documentation](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/installing/configuring-backup-restore-pvc-datamover.html)

### **OpenShift API for Data Protection (OADP) operator version is higher than the supported OpenShift cluster version**
- [See documentation](https://access.redhat.com/solutions/7138407)

### **OADP and  ODF Encrypted Volumes in OpenShift**
- When using kms encryption with ODF volumes the secrets related to the ODF encryption must first be copied to the OADP namespace ( e.g. openshfit-adp ) for backup and restore operations to work properly.   See related issue: https://redhat.atlassian.net/browse/OADP-7893

### **Unbound PVC and Pending pod after datamover restore**
If an application pod is left in the Pending state post-restore with an unbound PVC with a status indicating that a PV cannot be provisioned due to `spec.selector` being set, this is not a bug. The application PVC binds to the restored PV once the datamover pod has completed. Do not attempt to remove the selector from the PVC as a workaround. The root cause is that the DataDownload itself has not completed. You need to diagnose the problem there rather than looking at the application PVC.

### **Node Agent LoadAffinity is not applied to datamover pods in OADP 1.5**
In OADP 1.5, the loadAffinity parameter is used to limit the nodes on which Node Agent pods run. Unfortunately, the same restriction is not applied to the datamover pods which process DataUploads and DataDownloads. If one of these pods gets scheduled on a node which does not have a running node agent, the DataUpload or DataDownload will not be processed. The resolution is to upgrade to OADP 1.6 or newer. The workaround is not to use loadAffinity.

### **OADP supports short term token credentials (STS) across multiple cloud providers**
- ROSA / AWS, [docs](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/oadp-rosa/oadp-rosa-backing-up-applications.html)
- GCP workload identity federation WIF support, [docs](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/installing/installing-oadp-gcp.html#oadp-gcp-wif-cloud-authentication_installing-oadp-gcp)
   - **note** VSL, volumesnapshot locations is not supported with WIF
- Azure Security Token Service STS,  [doc](https://docs.okd.io/latest/backup_and_restore/application_backup_and_restore/installing/installing-oadp-azure.html#oadp-auth-azure-STS_installing-oadp-azure)
  - imagestream backups are NOT supported with Azure STS see [bug](https://github.com/openshift/openshift-velero-plugin/issues/439)
  -  **note** VSL, volumesnapshot locations is not supported with Azure STS.