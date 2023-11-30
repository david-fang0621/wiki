## 1. Edit hosts file

The `/etc/hosts` file on your local machine maps custom domain names to the IP addresses. It's protected, so you'll likely have to use `sudo` to open it and enter your Mac password.

To edit your hosts file in vim, open your preferred terminal and enter `sudo vim /etc/hosts`. You'll see something like:

```
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost

```

Don't delete anything, just add another line beneath the localhost line with your desired host name like this:

```
127.0.0.1       localhost
127.0.0.1       yoursite.loc

```

Then save the file and exit.

I like to end mine with .loc but you can use .dev or something else as well. It should be unique but easy for you to remember.

## 2. Edit MAMP Apache config file

Now go to the directory your MAMP install is located in. Mine is at `/Applications/MAMP` which is the default, so that's what I'll use as the path for the following examples.

Find the Apache config file at `/Applications/MAMP/conf/apache/httpd.conf` and open it in an editor. There's likely a bunch of stuff in here; scroll through and find these lines:

```
# Virtual hosts
# Include /Applications/MAMP/conf/apache/extra/httpd-vhosts.conf

```

All you need to do here is un-comment that second line, so it looks like this:

```
# Virtual hosts
Include /Applications/MAMP/conf/apache/extra/httpd-vhosts.conf

```

Save the file.

## 3. Edit your virtual hosts file

Next, open the virtual hosts file at `/Applications/MAMP/conf/apache/extra/httpd-vhosts.conf`.

There will probably be some comments and a couple of examples of blocks there. Leave the comments or delete as you'd like, then replace the examples with the information below. The second block includes the path to the site you're developing and the local domain name you added in the first step. So your file should look something like this:

```
NameVirtualHost *:80

<VirtualHost *:80>
    DocumentRoot "/Applications/MAMP/htdocs"
    ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "/Users/youruser/your/site/root"
    ServerName yoursite.loc
</VirtualHost>

```

## 4. You're Done!

Restart MAMP if it was running already and head to the domain you added. Your site should be live there!
