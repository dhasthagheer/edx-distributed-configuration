edx-distributed-configuration
=============================

Deploy edX services on different servers

sudo apt-get install -y build-essential software-properties-common python-software-properties curl git-core libxml2-dev libxslt1-dev python-pip python-apt python-dev sshpass 

sudo pip install --upgrade pip 

sudo pip install --upgrade virtualenv

cd /var/tmp

git clone https://github.com/dhasthagheer/edx-distributed-configuration.git configuration

sudo pip install -r /var/tmp/configuration/requirements.txt

cd /var/tmp/configuration/playbooks

vi /var/tmp/configuration/playbooks/inventory.ini

Edit the inventory file and give ip address of the servers in the respective groups

Installation
============

1. Mysql

sudo ansible-playbook -c ssh mysql.yml -i inventory.ini --limit mysql -e@server_vars.yml -u edx -k -K

2. Memcached

sudo ansible-playbook -c ssh memcached.yml -i inventory.ini --limit memcached -e@server_vars.yml -u edx -k -K

3. MongoDB

sudo ansible-playbook -c ssh mongo.yml -i inventory.ini --limit mongo -e@server_vars.yml -u edx -k -K

4. RabbitMQ

sudo ansible-playbook -c ssh rabbitmq.yml -i inventory.ini --limit rabbit_master -e@server_vars.yml -u edx -k -K

5. Elasticsearch

sudo ansible-playbook -c ssh elasticsearch.yml -i inventory.ini --limit elasticsearch -e@server_vars.yml -u edx -k -K

6. Xqueue

sudo ansible-playbook -c ssh xqueue.yml -i inventory.ini --limit xqueue -e@server_vars.yml  -u edx -k -K

7. ORA

sudo ansible-playbook -c ssh ora.yml -i inventory.ini --limit ora -e@server_vars.yml  -u edx -k -K

8. Certs

sudo ansible-playbook -c ssh certs.yml -i inventory.ini --limit certs -e@server_vars.yml  -u edx -k -K

9. CS_COMMENTS_SERVICE

sudo ansible-playbook -c ssh forum.yml -i inventory.ini --limit forum -e@server_vars.yml -u edx -k -K

10. LMS

sudo ansible-playbook -c ssh edxapp_lms.yml -i inventory.ini --limit lms -e@server_vars.yml  -u edx -k -K

11. CMS

sudo ansible-playbook -c ssh edxapp_cms.yml -i inventory.ini --limit cms -e@server_vars.yml  -u edx -k -K

12. Worker

sudo ansible-playbook -c ssh edxapp_worker.yml -i inventory.ini --limit workers -e@server_vars.yml  -u edx -k -K


Edx Production Installation with cluster
========================================

1. Mysql

sudo ansible-playbook -c ssh mysql.yml -i inventory.ini --limit mysql -e@server_vars.yml -u edx -k -K

2. Memcached

sudo ansible-playbook -c ssh memcached.yml -i inventory.ini --limit memcached -e@server_vars.yml -u edx -k -K

3. MongoDB cluster

sudo ansible-playbook -c ssh mongo.yml -i inventory.ini --limit mongo -e@server_vars.yml -u edx -k -K

Note: At the end you will get error on two secondary machines. Dont worry about the error. pymongo.errors.AutoReconnect: not master and slaveOk=false. Never mind it

4. Rabbit Server cluster

sudo ansible-playbook -c ssh rabbitmq.yml -i inventory.ini --limit rabbit_master,rabbit_slave1,rabbit_slave2 -e@server_vars.yml -u edx -k -K

5. Elasticsearch cluster

sudo ansible-playbook -c ssh elasticsearch.yml -i inventory.ini --limit elasticsearch -e@server_vars.yml -u edx -k -K

6. Xqueue

sudo ansible-playbook -c ssh xqueue.yml -i inventory.ini --limit xqueue -e@server_vars.yml  -u edx -k -K

7. ORA

sudo ansible-playbook -c ssh ora.yml -i inventory.ini --limit ora -e@server_vars.yml  -u edx -k -K

8. Certs

sudo ansible-playbook -c ssh certs.yml -i inventory.ini --limit certs -e@server_vars.yml  -u edx -k -K

9. CS_COMMENTS_SERVICE

sudo ansible-playbook -c ssh forum.yml -i inventory.ini --limit forum -e@server_vars.yml -u edx -k -K

10. LMS

sudo ansible-playbook -c ssh edxapp_lms.yml -i inventory.ini --limit lms -e@server_vars.yml  -u edx -k -K

11. CMS

sudo ansible-playbook -c ssh edxapp_cms.yml -i inventory.ini --limit cms -e@server_vars.yml  -u edx -k -K

12. Worker

sudo ansible-playbook -c ssh edxapp_worker.yml -i inventory.ini --limit workers -e@server_vars.yml  -u edx -k -K

XII. Nginx Load Balancer for LMS

sudo ansible-playbook -c ssh loadbalance.yml -i inventory.ini --limit lmsloadbalancer -e@server_vars.yml -e 'appname=lms  lms1_host=192.168.1.134 lms2_host=192.168.1.135 '  -u edx -k -K

XIII. Nginx Load Balancer for CMS

sudo ansible-playbook -c ssh loadbalance.yml -i inventory.ini --limit cmsloadbalancer -e@server_vars.yml -e 'appname=cms  cms1_host=192.168.1.136 cms2_host=192.168.1.137 '  -u edx -k -K




