# netapp_ansible_collections_templates
 Universal templates for NetApp Ansible Modules


What is this and why would I use it?

The objective allows users to rapidly prototype and build complete complex ontap collections commands without additional modifications. 

The play allows users to uncomment whatever vars are required and use the include_tasks to run each task. This allows you to add a loop statement to each play without duplicating tasks over and over again or needed to constantly lookup or define additional parameters per play. 
**How to run

ansible-playbook 

**Example 1:
Creates a complete volume create command.

cat head.yml vars/na_ontap_volume_vars.yml main.yml play/na_ontap_volume_play.yml >create_new_netapp_volume.yml


**Example 2:
How do you loop through multiple volumes/lifs/interfaces ... use the multi_ task which requires a loop item from a array. 

Creating a loop for multiple volumes. 
The following commands will help create and setup multivolume play.
cat head.yml vars/na_ontap_volume_vars.yml main.yml play/na_ontap_volume_play.yml >multi_create_vol_ntap.yml
sed -i 's/{{ /{{ item./' multi_create_vol_ntap.yml
sed -i 's/    validate_certs:/    #validate_certs:/' multi_create_vol_ntap.yml 
sed -i 's/tasks\/na_/tasks\/multi_na_/' multi_create_vol_ntap.yml 
echo '      loop: "{{ ntap_volumes }}"'>>multi_create_vol_ntap.yml

copy this to the bottom of the vars section and update for your environment.  
    ntap_volumes:
     - {"req_volume_name_01":"ansible_vol01","req_volume_vserver_01":"svm05","opt_volume_size_01":"12","opt_volume_size_unit_01":"gb","opt_volume_junction_path_01":"/ansible_vol01","opt_volume_volume_security_style_01":"unix","opt_volume_aggregate_name_01":"Data_Aggr01","opt_volume_space_guarantee_01":"none"}
     - {"req_volume_name_01":"ansible_vol02","req_volume_vserver_01":"svm05","opt_volume_size_01":"12","opt_volume_size_unit_01":"gb","opt_volume_junction_path_01":"/ansible_vol02","opt_volume_volume_security_style_01":"unix","opt_volume_aggregate_name_01":"Data_Aggr01","opt_volume_space_guarantee_01":"none"}
     - {"req_volume_name_01":"ansible_vol03","req_volume_vserver_01":"svm05","opt_volume_size_01":"12","opt_volume_size_unit_01":"gg","opt_volume_junction_path_01":"/ansible_vol03","opt_volume_volume_security_style_01":"unix","opt_volume_aggregate_name_01":"Data_Aggr01","opt_volume_space_guarantee_01":"none"}
