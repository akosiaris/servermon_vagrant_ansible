servermon vagrant ansible
=========================

Servermon vagrant ansible is a vagrant project that uses ansible to
create a 4 machine environment and deploy servermon to it. The
architecture is:

* 2 Application servers running django
* 1 MySQL database server
* 1 Loadbalancer routing to the 2 application servers.

All VMs are Debian Jessie 64-bit

The load balancer is implemented using an nginx server

The application servers use uwsgi

servermon
=========

Servermon is a Django project with the aim of facilitating server monitoring
and management through Puppet. The place where servermon is developed is at
http://github.com/servermon/servermon

Usage
=====

Make sure you got vagrant and virtualbox. Vagrant version required is at least
1.7 so you if you are using Debian Wheezy you will have to download the .deb
manually. Virtualbox version used during development is 4.3, it might be best to
stick to that, as I have done zero testing with other versions

.. code-block:: bash
    vagrant up
    vagrant ssh lb01 ip addr ls dev eth1

Get the IP listed there

Then point your browser to:

http://<IP>

and you should get a servermon view filled with sample data
