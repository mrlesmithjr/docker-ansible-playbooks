#Builds Ubuntu Apt-Cacher-NG image

#FROM mrlesmithjr/ansible:ubuntu-12.04
FROM mrlesmithjr/ansible:ubuntu-14.04

MAINTAINER mrlesmithjr@gmail.com

VOLUME      ["/var/cache/apt-cacher-ng"]

#Installs git
RUN apt-get update && apt-get install -y \
  git \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#Clean up Ansible playbooks
RUN rm -rf /opt/ansible-playbooks

#Clone docker ansible playbooks from GitHub
RUN git clone https://github.com/mrlesmithjr/docker-ansible-playbooks.git /opt/ansible-playbooks/

#Install Ansible role requirements
RUN ansible-galaxy install -r /opt/ansible-playbooks/apt-cacher-ng/requirements.yml

#Run Ansible playbook to install Apt-Cacher-NG
RUN ansible-playbook -i "localhost," -c local /opt/ansible-playbooks/apt-cacher-ng/playbook.yml --extra-vars="apt_cacher_server=localhost"

#Remove Ansible roles
RUN ansible-galaxy remove /etc/ansible/roles/*

#Clean up Ansible Playbooks
RUN rm -rf /opt/ansible-playbooks

#Clean up APT
RUN apt-get clean

#Expose ports
EXPOSE 3142

CMD     chmod 777 /var/cache/apt-cacher-ng && /etc/init.d/apt-cacher-ng start && tail -f /var/log/apt-cacher-ng/*
