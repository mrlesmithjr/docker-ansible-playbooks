#Builds Ubuntu Apache2 image

#Uses ubuntu:14.04.3 with ansible installed
FROM mrlesmithjr/ubuntu-14.04.3-ansible

MAINTAINER mrlesmithjr@gmail.com

#Installs git
RUN apt-get update && apt-get install -y \
  git \
  && apt-get clean \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#Clone docker ansible playbooks from GitHub
RUN git clone https://github.com/mrlesmithjr/docker-ansible-playbooks.git /opt/ansible-playbooks/

RUN ansible-playbook /opt/ansible-playbooks/apache2/apache2.yml -c local

EXPOSE 80

ENTRYPOINT ["apache2ctl"]

CMD ["-D", "FOREGROUND"]
