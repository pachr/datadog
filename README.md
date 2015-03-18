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

and put in it the DNS or IP address of the hosts in the correct host group

###How to run the playbook

* To install the datadog agent on all host

```
ansible-playbook -i hosts datadog_playbook.yml --extra-vars "hosts=all" --private-key=~/path/to/private/key
```
Possible tags  :

- datadog-<tags>

	* agent
	* mongo
	* pgsql
	* memcached
	* solr
	* tomcat 
	* jvm
	* rabbitmq
	* nginx
	* dogstatsd

Example :

```
ansible-playbook -i hosts datadog_playbook.yml --tags "datadog-mongo" --private-key=~/path/to/private/key
```

Notes :

We can --skip-tags also
--extra-vars "hosts=all" is required for datadog-agent role only
other roles have them hosts specified in the play (See Inventory file section above)

##Requirements

Files in env_vars folder are encrypted 

These files contains environment variables, passwords, usernames, and API keys, this is the content of each file :

* datadog-agent/staging.yml
	- datadog_api_key: specify your datadog API key

* datadog-jvm/staging.yml
	- datadog_jmx_instance: jmx_instance
	- datadog_jmx_username: username 
	- datadog_jmx_password: password 

* datadog-mongo/staging.yml
	- datadog_mongo_user_pass: specify your user password (We create a read-only user with the username : datadog as specify in datadog documentation)

* datadog-nginx/staging.yml
	- nginx_dir: specify the nginx directory (where the nginx http_stub_status_module is located)
	// path: "{{nginx_dir}}/sites-enabled/nginx_status"
    // src: "{{nginx_dir}}/sites-available/nginx_status"

* datadog-pgsql/staging.yml
	- datadog_pgsql_user_pass: same as mongo

* datadog-rabbitmq/staging.yml
	- rabbitmq_user_pass: same as mongo

* datadog-solr/staging.yml
	- datadog_solr_username: solr_username
	- datadog_solr_user_pass: solr_user_password
	- datadog_solr_instance: solr_instance

* datadog-tomcat/staging.yml
	- datadog_tomcat_username: tomcat_username
	- datadog_tomcat_user_pass: tomcat_user_password
	- datadog_tomcat_instance: tomcat_instance

##Other requirements

- We need to speak about RabbitMQ : User creation, I'm not sure
- Fill out the inventory file to run the playbook on Noodle 
- Test if my roles are correct
- Update all security groups : open the port 17123 for datadog agent and 8125 for dogstatsd



