# gvk-upgrade

Sample playbook showing the workflow for performing GVK conversion.

## Usage

|Steps|
|---|
|1. Run a migration with [mig-controller](https://github.com/konveyor/mig-controller)|
|2. Take note of the MigPlan name used, as well as the S3 bucket name| 
|2. Supply values for the ansible vars `migplan_name` and `bucket_name` by editing playbook.yml or using ansible extra vars|
|3. Ensure you have a new enough `oc` client version to perform the conversion (should match newer cluster involved in migration)|
|4. Run the playbook|

## Output
Converted files will be dropped in a new directory `convert_complete`.

## Limitations
- This playbook is an illustrative sample, and only works with S3 compatible MigStorage backends
- This playbook doesn't verify that your installed `oc` version configured on `$PATH` can perform the required conversion.  
  - Start with the destination cluster `oc` client version
  - If the destination cluster `oc` client version doesn't work, keep trying, dropping back 1 minor `oc` release each time. E.g. if destination cluster is 4.4, try using oc versions (4.4, 4.3, 4.2, 4.1, ...) until a version is found capable of the  offline GVK conversion.
