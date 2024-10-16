# poc-manage-hybrid-park-with-awx

Here is to give a way to manage windows and linux machines with same AWX/Tower job template

Playbook.yml: contains a playbook example to distinguish between linux and windows machines in a flat inventory (n grouping and no possibility to modify inventory to add host vars or ...)

ansible_user and ansible_password ... variables are filled with environement variables that were injected by awx/ansible in the execution environment of job template

Vagrantfile: for creation of two machines (windows and linux) for testing purposes

Demo is on video in this repo
