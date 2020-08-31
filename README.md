# netapp_ansible_collections_templates
 Universal templates for NetApp Ansible Modules


What is this and why would I use it?

The objective allows users to rapidly prototype and build complete complex ontap collections commands without additional modifications. 

The play allows users to uncomment whatever vars are required and use the include_tasks to run each task. This allows you to add a loop statement to each play without duplicating tasks over and over again or needed to constantly lookup or define additional parameters per play. 
**How to run**

**Example 1:**
Creates a complete volume create command.
```
cat head.yml ontap/vars/na_ontap_volume_vars.yml main.yml ontap/play/na_ontap_volume_play.yml >create_new_netapp_volume.yml
```
```
ansible-playbook multi_create_vol_ntap.yml -e "netapp_hostname=cluster1" -e "netapp_username=admin" -e "netapp_password=Secret123^"
```

**Example 2:**
How do you loop through multiple volumes/lifs/interfaces ... Use the /task/multi_ task to run the command.

Creating a loop for multiple volumes. 
The following commands will help create and setup multivolume play for a example that can be use for other plays.
```
cat head.yml ontap/vars/na_ontap_volume_vars.yml main.yml ontap/play/multi_na_ontap_volume_play.yml >multi_create_vol_ntap.yml
add 
     loop: {{ ntap_volumes }}

after the task line and your all set.

```
copy this to the bottom of the vars section and update for your environment.  
```
    ntap_volumes:
     - {"req_volume_name_01":"ansible_vol01","req_volume_vserver_01":"svm05","opt_volume_size_01":"12","opt_volume_size_unit_01":"gb","opt_volume_junction_path_01":"/ansible_vol01","opt_volume_volume_security_style_01":"unix","opt_volume_aggregate_name_01":"Data_Aggr01","opt_volume_space_guarantee_01":"none"}
     - {"req_volume_name_01":"ansible_vol02","req_volume_vserver_01":"svm05","opt_volume_size_01":"12","opt_volume_size_unit_01":"gb","opt_volume_junction_path_01":"/ansible_vol02","opt_volume_volume_security_style_01":"unix","opt_volume_aggregate_name_01":"Data_Aggr01","opt_volume_space_guarantee_01":"none"}
     - {"req_volume_name_01":"ansible_vol03","req_volume_vserver_01":"svm05","opt_volume_size_01":"12","opt_volume_size_unit_01":"gb","opt_volume_junction_path_01":"/ansible_vol03","opt_volume_volume_security_style_01":"unix","opt_volume_aggregate_name_01":"Data_Aggr01","opt_volume_space_guarantee_01":"none"}
```
**And run the commands**
```
ansible-playbook multi_create_vol_ntap.yml -e "netapp_hostname=cluster1" -e "netapp_username=admin" -e "netapp_password=Secret123^"
```
```
