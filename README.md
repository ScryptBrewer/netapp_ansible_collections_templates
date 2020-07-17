# netapp_ansible_collections_templates
 Universal templates for Netapp Ansible Modules


What is this and why would I use it?

my concept is to scrape the help from the latest greatest netapp collecitons for ansible and create a rapid prototype template system. 

users should be able to quickly create a complete complex play without significat effort and reproduce these in the future as needed!

The play allows users to uncomment whatever vars are required and use the include_task to run each task. This allows you to add a loop statment to each play without duplicating tasks over and over again or needed to contstatly lookup or define addtional parameters per play. 

a simple example of how you can use this would be:

cat head.yml vars/na_ontap_volume_vars.yml main.yml play/na_ontap_volume_play.yml >VolCreatePlay.yml




 
