# datadog integrations with ansible

##Usage 

###Content

This repo contains one playbook 'datadog_playbook.yml'

Inside this playbook we can find :

- A role to install datadog agent on hosts (Specify hosts in extra vars --extra-vars "hosts=prod" for example)
- Multiple roles to install datadog integrations
	* Dogstatsd
	* JVM (Java Virtual machine)
	* Memcached
	* Mongo
	* Nginx
	* PostgreSQL
	* RabbitMQ
	* Solr
	* Tomcat7

###Inventory file

Inventory file name : hosts
groups : We must have a group per integration

* Dogstatsd
* JVM (Java Virtual machine)
* Memcached
* Mongo
* Nginx
* PostgreSQL
* RabbitMQ
* Solr
* Tomcat7

and put in it the DNS or IP address of the hosts in correct host group

###How to run the playbook

* To install the datadog agent on all host

```
ansible-playbook -i hosts datadog_playbook.yml --extra-vars "hosts=all" --private-key=~/path/to/private/key -vvvv
```

