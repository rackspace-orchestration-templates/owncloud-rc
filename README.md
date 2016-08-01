[![Circle CI](https://circleci.com/gh/rackspace-orchestration-templates/owncloud/tree/master.png?style=shield)](https://circleci.com/gh/rackspace-orchestration-templates/owncloud)
Description
===========

This is a template for deploying a [ownCloud](http://owncloud.org/) on a single
Linux Server.

Requirements
============
* A Heat provider that supports the Rackspace `OS::Heat::ChefSolo` plugin.
* An OpenStack username, password, and tenant id.
* [python-heatclient](https://github.com/openstack/python-heatclient)
`>= v0.2.8`:

```bash
pip install python-heatclient
```

We recommend installing the client within a [Python virtual
environment](http://www.virtualenv.org/).

Example Usage
=============
Here is an example of how to deploy this template using the
[python-heatclient](https://github.com/openstack/python-heatclient):

```
heat --os-username <OS-USERNAME> --os-password <OS-PASSWORD> --os-tenant-id \
  <TENANT-ID> --os-auth-url https://identity.api.rackspacecloud.com/v2.0/ \
  stack-create ownCloud-Stack -f owncloud.yaml \
  -P flavor="4 GB Performance"
```

* For UK customers, use `https://lon.identity.api.rackspacecloud.com/v2.0/` as
the `--os-auth-url`.

Optionally, set environmental variables to avoid needing to provide these
values every time a call is made:

```
export OS_USERNAME=<USERNAME>
export OS_PASSWORD=<PASSWORD>
export OS_TENANT_ID=<TENANT-ID>
export OS_AUTH_URL=<AUTH-URL>
```

Parameters
==========
Parameters can be replaced with your own values when standing up a stack. Use
the `-P` flag to specify a custom parameter.

* `image`: Operating system to install (Default: Ubuntu 14.04 LTS (Trusty
  Tahr))
* `flavor`: Cloud server size to use. (Default: 2 GB Performance)
* `owncloud_username`: Admin username to configure with ownCloud (Default:
  admin)
* `kitchen`: URL for the kitchen to clone with git. The Chef Solo run will copy
  all files in this repo into the kitchen for the chef run. (Default:
  https://github.com/rackspace-orchestration-templates/owncloud)
* `chef_version`: Chef client version to install for the chef run.  (Default:
  11.12.8)

Note: The admin password will be automatically generated and passed back to you
as an output.

Outputs
=======
Once a stack comes online, use `heat output-list` to see all available outputs.
Use `heat output-show <OUTPUT NAME>` to get the value fo a specific output.

* `private_key`: SSH private that can be used to login as root to the server.
* `server_ip`: Public IP address of the cloud server
* `owncloud_url`: Address to use when accessing ownCloud
* `owncloud_username`: Admin username to use for logging into ownCloud
* `owncloud_password`: Admin password to use for logging into ownCloud
* `mysql_root_password`: MySQL Root Password
* `owncloud_db_password`: Database password for the ownCloud database

For multi-line values, the response will come in an escaped form. To get rid of
the escapes, use `echo -e '<STRING>' > file.txt`. For vim users, a substitution
can be done within a file using `%s/\\n/\r/g`.

Stack Details
=============
#### Getting Started
If you are new to [ownCloud](http://owncloud.org/), check out their
documentation on how to use the [web
interface](http://doc.owncloud.org/server/6.0/user_manual/webinterface.html).

#### Accessing your Deployment
Use the ownCloud URL provided to access your deployment. You will get a
certificate warning since it's self signed. Login with the ownCloud username
and password provided.

#### Logging in via SSH
The private key provided in the passwords section can be used to login as
root via SSH.  We have an article on how to use these keys with [Mac OS X and
Linux](http://www.rackspace.com/knowledge_center/article/logging-in-with-a-ssh-private-key-on-linuxmac)
as well as [Windows using
PuTTY](http://www.rackspace.com/knowledge_center/article/logging-in-with-a-ssh-private-key-on-windows).

Contributing
============
There are substantial changes still happening within the [OpenStack
Heat](https://wiki.openstack.org/wiki/Heat) project. Template contribution
guidelines will be drafted in the near future.

License
=======
```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
