# docker18.09.1
This ansible role will install Docker version 18.09.1, build 4c52b90 and setup docker users on Centos, Redhat and Fedora.

Requirements
ansible installation

Role Variables

Available variables are listed below, along with variables 
vars/main.yml

# Edition can be one of: 'ce' (Community Edition) or 'ee' (Enterprise Edition).
docker_edition: 'ce'
docker_package: "docker-{{ docker_edition }}"
docker_package_state: present

The docker_edition should be either ce (Community Edition) or ee (Enterprise Edition). 

docker_service_state: started
docker_service_enabled: true
docker_restart_handler_state: restarted

Variables to control the state of the docker service, and whether it should start on boot. If you're installing Docker inside a Docker container without systemd or sysvinit, you should set these to stopped and set the enabled variable to no.

docker_install_compose: false
docker_compose_version: "1.22.0"
docker_compose_path: /usr/local/bin/docker-compose

Docker Compose installation options.

(Used only for RedHat/CentOS.) You can enable the Edge or Test repo by setting the respective vars to 1.
docker_yum_repo_url: https://download.docker.com/linux/{{ (ansible_distribution == "Fedora") | ternary("fedora","centos") }}/docker-{{ docker_edition }}.repo
docker_yum_repo_enable_edge: 0
docker_yum_repo_enable_test: 0

A list of system users to be added to the docker group (so they can use Docker on the server).
docker_users:
  - user1
  - user2

Dependencies
Example Playbook : ~/ansible/playbooks/test.yml

---
- hosts: all
  become: true

  roles:
    - docker

License

MIT / BSD
