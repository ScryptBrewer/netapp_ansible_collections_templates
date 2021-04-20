# netapp_ansible_collections_templates
 Universal templates for NetApp Ansible Modules


What is this and why would I use it?

The NetApp ansible modules are complete and offer many choices however, starting from zero or needing a buch of looped activites can  be daughting. This framework allows users to quicky comsume netapp plays and setting up either CSV sources or a dictonary based varible to add and remove parameters per item in dictionary.  

**How to run**

**Example 1:**
Creates a complete volume create command.
```
cat head.yml ontap/play/na_ontap_volume_play.yml >create_new_netapp_volume.yml
Update your play to include the desired varibles and delete the rest. 
Note if your only doing a single item you can remove the loop parameter and update the vars directly. 
```
```
ansible-playbook multi_create_vol_ntap.yml -e "netapp_hostname=cluster1" -e "netapp_username=admin" -e "netapp_password=Secret123^"
```

**Example 2:**
How do you loop through multiple volumes/lifs/interfaces 

Creating a loop for multiple volumes. 
The following commands will help create and setup multivolume play for a example that can be use for other plays.
```
cat head.yml ontap/play/multi_na_ontap_volume_play.yml >multi_create_vol_ntap.yml

update the loop name to your var
     loop: {{ ntap_volumes }}

after the task line and your all set.

```
copy this to the bottom of the vars section and update for your environment or import a csv as your first task.
```
   ntap_volumes:
     - {"name":"ansible_vol01","vserver":"svm05","size":"12","size_unit":"gb","junction_path":"/ansible_vol01","security_style":"unix","aggregate_name":"Data_Aggr01","space_guarantee":"none"}
     - {"name":"ansible_vol02","vserver":"svm05","size":"12","size_unit":"gb","junction_path":"/ansible_vol02","security_style":"unix","aggregate_name":"Data_Aggr01","space_guarantee":"none"}
     - {"name":"ansible_vol03","vserver":"svm05","size":"12","size_unit":"gb","junction_path":"/ansible_vol03","security_style":"unix","aggregate_name":"Data_Aggr01","space_guarantee":"none"}
```
**And run the commands**
```
ansible-playbook multi_create_vol_ntap.yml -e "netapp_hostname=cluster1" -e "netapp_username=admin" -e "netapp_password=Secret123"
```
```
