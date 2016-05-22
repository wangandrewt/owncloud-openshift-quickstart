ownCloud on OpenShift
=========================

ownCloud is a flexible, open source file sync and share solution. Whether using a mobile device, a workstation, or a web client, ownCloud provides the ability to put the right files at their employees’ fingertips on any device in one simple-to-use, secure, private and controlled solution.

Think of ownCloud as a way to roll your own Google Drive or Dropbox on-premise solution.

More information can be found at http://owncloud.org/

About this Fork
---------

This fork supports upgrading between ownCloud versions. Update `install_version` in *.openshift/action_hooks/build*, commit the change, push to your OpenShift, and open the application in your browser to complete the upgrade.

Previous ownCloud versions will not be removed from *${OPENSHIFT_DATA_DIR}/current*. Delete them after finishing the upgrade.

1. SSH to Openshift: `rhc ssh -a <app-name>`
1. Change to *${OPENSHIFT_DATA_DIR}/current*: `cd app-root/data/current`
1. Remove the old directory: `rm -r <old-version>`

Running on OpenShift
--------------------

Create an account at https://www.openshift.com

Create a PHP application with a MySQL cartridge:

	rhc app create owncloud php-5.4 mysql-5.5 cron-1.4

or with PostgreSQL cartridge:

	rhc app create owncloud php-5.4 postgresql-9.2 cron-1.4

Add this upstream ownCloud quickstart repo

	cd owncloud
	git remote add upstream -m master git://github.com/wangandrewt/owncloud-openshift-quickstart.git
	git pull -s recursive -X theirs upstream master

Push back to your OpenShift repo

	git push

Head to your application at:

	http://owncloud-$yourdomain.rhcloud.com

Default Credentials
-------------------

The default user is 'admin' and the password should be printed out to console
after deployment. Please change the default password after first login.

To download clients that will sync your ownCloud instance with desktop clients, visit http://owncloud.org/sync-clients/

To give your new ownCloud site a web address of its own, add your desired alias:

	rhc app add-alias -a owncloud --alias "$whatever.$mydomain.com"

Then add a cname entry in your domain's dns configuration pointing your alias to $whatever-$yourdomain.rhcloud.com.
