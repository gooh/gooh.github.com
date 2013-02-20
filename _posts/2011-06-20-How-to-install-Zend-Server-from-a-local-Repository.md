---

layout: post
title: How to install Zend Server from a local Repository
tagline: a guide for the perplexed
tags: [linux, zend, guide]

---

The following is a guide to do a manual install of Zend Server on RHEL 5/6. I needed this solution because I had to install Zend Server on a machine in an intranet with no WAN and the Zend Website only offered an RPM installer that required an internet connection.

*Disclaimer: Note that the solution below worked for me. It doesn't mean it will work for you. If you break something in the process, it's not my fault. When in doubt, buy Zend Support.*

##Step 1 - Mirror the Zend Server Repository

When you are using the installer script, it will try to download the appropriate Zend Server sources from

- http://repos-source.zend.com/zend-server/rpm/

so open a command prompt and mirror that location

    wget --mirror --no-parent http://repos-source.zend.com/zend-server/rpm/

This will download *all* files at that location, including any optional extensions and some cruft. If you know
your required cpu architecture, you can limit wget to mirror only the appropriate folders. Once you hit Enter,
go make a coffee or something because this will take a while (about 315MB for Zend Server 5.1).

Upload the file to the target machine when done.

##Step 2 - Download the RPM installer

You can get this one from the zend.com Download section. When done, upload and extract the archive on the target machine

    tar xzf /downloads/ZendServer-RepositoryInstaller-linux.tar.gz

This will create the folder `ZendServer-RepositoryInstaller` in `/downloads` with all the contents of the archive.
`cd` into that directory now.

##Step 3 - Modify the repository file

You now have all the required files. Move the mirrored rpm folder to some convenient location, like
`/opt/zend-server/rpm` or whatever you deem convenient. Then tell your RHEL about the new location.

Modify `zend.rpm.repo` to read the following:

```ini
[Zend]
name=Zend Server
baseurl=file:///opt/zend-server/rpm/$basearch
enabled=1
gpgcheck=0
gpgkey=http://repos.zend.com/zend.key

[Zend_noarch]
name=Zend Server - noarch
baseurl=file:///opt/zend-server/rpm/noarch
enabled=1
gpgcheck=0
gpgkey=http://repos.zend.com/zend.key
```

##Step 4 - Install from the local repository

After you have made the changes to repo files, installing takes the same steps explained in the
Installation Guide. If you are **not** on SELinux you can skip the following step

    setenforce permissive

To install Zend Server, call the install script with the desired version, e.g. for 5.3 do

    ./install_zs.sh 5.3

Confirm any prompts with yes.

Zend Server should now be running at these URIs

- https://localhost:10082/ZendServer (secure)
- http://localhost:10081/ZendServer (non-secure)

And that's it. You can do a `yum clean all` to clean up any meta data if you want and add PHP to your PATH environment to make it available on CLI now. Details for that can be found in the Installation Guide.

## Alternative without the installer script

Instead of using the installer script, you can also add the `zend.rpm.repo` file to `/etc/yum.repos.de/` and then do a `yum install` manually. This is the same as explained in the Installation Guide. The only difference is the local repository.

## Additional Packages

Because you mirrored the full repository, you will also have all the optional packages now. You can install any
of those with a regular `yum install package-name`. For the full list of additional packages, see

- http://static.zend.com/topics/server/Zend-Server-Installation-Guide.pdf

## Troubleshooting

Error: Metadata file does not match checksum. Trying other mirror
Solution: `yum clean all`

Error: php-5.3-page_cache-&hellip; not found
Solution: check the given path and make sure the file does not contain url encoded values, e.g. `%3a` instead of `:`

## Updating and Uninstalling Zend Server

Since your Zend Repo points to a local repository, you won't get any updates. You have to replace updated content in the repository manually. Uninstalling works the same as with a non-local repository. See the Installation Guide for details.