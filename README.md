# docker18.09.1
This ansible role will install Docker version 18.09.1, build 4c52b90 and setup docker users on Centos, Redhat and Fedora.<br/>
<br/>
Requirements<br/>
ansible installation<br/>
<br/>
Role Variables
<br/>
Available variables are listed below, along with variables <br/>
vars/main.yml<br/>
<br/>
### Edition can be one of: 'ce' (Community Edition) or 'ee' (Enterprise Edition).<br/>
docker_edition: 'ce'<br/>
docker_package: "docker-{{ docker_edition }}"<br/>
docker_package_state: present<br/>
<br/>
The docker_edition should be either ce (Community Edition) or ee (Enterprise Edition). <br/>
<br/>
docker_service_state: started<br/>
docker_service_enabled: true<br/>
docker_restart_handler_state: restarted<br/>
<br/>
Variables to control the state of the docker service, and whether it should start on boot. If you're installing Docker inside a Docker container without systemd or sysvinit, you should set these to stopped and set the enabled variable to no.<br/>
<br/>
docker_install_compose: false<br/>
docker_compose_version: "1.22.0"<br/>
docker_compose_path: /usr/local/bin/docker-compose<br/>
<br/>
Docker Compose installation options.<br/>
<br/>
(Used only for RedHat/CentOS.) You can enable the Edge or Test repo by setting the respective vars to 1.<br/><br/>
docker_yum_repo_url: https://download.docker.com/linux/{{ (ansible_distribution == "Fedora") | ternary("fedora","centos") }}/docker-{{ docker_edition }}.repo<br/>
<br/>
docker_yum_repo_enable_edge: 0<br/>
docker_yum_repo_enable_test: 0<br/>
<br/>
A list of system users to be added to the docker group (so they can use Docker on the server).<br/>
docker_users:<br/>
<pre>
  - user1
  - user2
</pre>
Dependencies<br/>
Example Playbook : ~/ansible/playbooks/test.yml<br/>
<pre>
---
- hosts: all
  become: true

  roles:
    - docker

</pre>
License
<br/>
MIT / BSD
