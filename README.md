###Edx-Distributed-Configuration


<b>Deploy edX</b>

<pre>sudo apt-get install -y build-essential software-properties-common python-software-properties curl git-core libxml2-dev libxslt1-dev python-pip python-apt python-dev sshpass 

sudo pip install --upgrade pip 

sudo pip install --upgrade virtualenv

cd /var/tmp

git clone https://github.com/dhasthagheer/edx-distributed-configuration.git configuration

sudo pip install -r /var/tmp/configuration/requirements.txt

cd /var/tmp/configuration/playbooks

vi /var/tmp/configuration/playbooks/inventory.ini
</pre>

Edit the inventory file and give ip address of the servers in the respective groups

<b>Installation</b>

######1. Mysql

<pre>sudo ansible-playbook -c ssh mysql.yml -i inventory.ini --limit mysql -e@server_vars.yml -u edx -k -K</pre>

######2. Memcached

<pre>sudo ansible-playbook -c ssh memcached.yml -i inventory.ini --limit memcached -e@server_vars.yml -u edx -k -K</pre>

######3. MongoDB

<pre>sudo ansible-playbook -c ssh mongo.yml -i inventory.ini --limit mongo -e@server_vars.yml -u edx -k -K</pre>

######4. RabbitMQ

<pre>sudo ansible-playbook -c ssh rabbitmq.yml -i inventory.ini --limit rabbit_master -e@server_vars.yml -u edx -k -K</pre>

######5. Elasticsearch

<pre>sudo ansible-playbook -c ssh elasticsearch.yml -i inventory.ini --limit elasticsearch -e@server_vars.yml -u edx -k -K </pre>

######6. Xqueue

<pre>sudo ansible-playbook -c ssh xqueue.yml -i inventory.ini --limit xqueue -e@server_vars.yml  -u edx -k -K</pre>

######7. ORA

<pre>sudo ansible-playbook -c ssh ora.yml -i inventory.ini --limit ora -e@server_vars.yml  -u edx -k -K</pre>

######8. Certs

<pre>sudo ansible-playbook -c ssh certs.yml -i inventory.ini --limit certs -e@server_vars.yml  -u edx -k -K</pre>

######9. CS_COMMENTS_SERVICE

<pre>sudo ansible-playbook -c ssh forum.yml -i inventory.ini --limit forum -e@server_vars.yml -u edx -k -K</pre>

######10. LMS

<pre>sudo ansible-playbook -c ssh edxapp_lms.yml -i inventory.ini --limit lms -e@server_vars.yml  -u edx -k -K</pre>

######11. CMS

<pre>sudo ansible-playbook -c ssh edxapp_cms.yml -i inventory.ini --limit cms -e@server_vars.yml  -u edx -k -K</pre>

######12. Worker

<pre>sudo ansible-playbook -c ssh edxapp_worker.yml -i inventory.ini --limit workers -e@server_vars.yml  -u edx -k -K</pre>


####Edx Production Installation with cluster


######1. Mysql

<pre>sudo ansible-playbook -c ssh mysql.yml -i inventory.ini --limit mysql -e@server_vars.yml -u edx -k -K</pre>

######2. Memcached

<pre>sudo ansible-playbook -c ssh memcached.yml -i inventory.ini --limit memcached -e@server_vars.yml -u edx -k -K</pre>

######3. MongoDB cluster

<pre>sudo ansible-playbook -c ssh mongo.yml -i inventory.ini --limit mongo -e@server_vars.yml -u edx -k -K</pre>

Note: At the end you will get error on two secondary machines. Dont worry about the error. pymongo.errors.AutoReconnect: not master and slaveOk=false. Never mind it

######4. Rabbit Server cluster

<pre>sudo ansible-playbook -c ssh rabbitmq.yml -i inventory.ini --limit rabbit_master,rabbit_slave1,rabbit_slave2 -e@server_vars.yml -u edx -k -K</pre>

######5. Elasticsearch cluster

<pre>sudo ansible-playbook -c ssh elasticsearch.yml -i inventory.ini --limit elasticsearch -e@server_vars.yml -u edx -k -K</pre>

######6. Xqueue

<pre>sudo ansible-playbook -c ssh xqueue.yml -i inventory.ini --limit xqueue -e@server_vars.yml  -u edx -k -K</pre>

######7. ORA

<pre>sudo ansible-playbook -c ssh ora.yml -i inventory.ini --limit ora -e@server_vars.yml  -u edx -k -K</pre>

######8. Certs

<pre>sudo ansible-playbook -c ssh certs.yml -i inventory.ini --limit certs -e@server_vars.yml  -u edx -k -K</pre>

######9. CS_COMMENTS_SERVICE

<pre>sudo ansible-playbook -c ssh forum.yml -i inventory.ini --limit forum -e@server_vars.yml -u edx -k -K</pre>

######10. LMS

<pre>sudo ansible-playbook -c ssh edxapp_lms.yml -i inventory.ini --limit lms -e@server_vars.yml  -u edx -k -K</pre>

######11. CMS

<pre>sudo ansible-playbook -c ssh edxapp_cms.yml -i inventory.ini --limit cms -e@server_vars.yml  -u edx -k -K</pre>

######12. Worker

<pre>sudo ansible-playbook -c ssh edxapp_worker.yml -i inventory.ini --limit workers -e@server_vars.yml  -u edx -k -K</pre>

######13. Nginx Load Balancer for LMS

<pre>sudo ansible-playbook -c ssh loadbalance.yml -i inventory.ini --limit lmsloadbalancer -e@server_vars.yml -e 'appname=lms  lms1_host=192.168.1.134 lms2_host=192.168.1.135 '  -u edx -k -K </pre>

######14. Nginx Load Balancer for CMS

<pre>sudo ansible-playbook -c ssh loadbalance.yml -i inventory.ini --limit cmsloadbalancer -e@server_vars.yml -e 'appname=cms  cms1_host=192.168.1.136 cms2_host=192.168.1.137 '  -u edx -k -K</pre>




