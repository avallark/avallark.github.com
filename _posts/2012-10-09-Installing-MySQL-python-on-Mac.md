---
layout: post.html
author: Abdul Bijur Vallarkodath
title: Installing python, mysql and python-mysql on a Mac
---

Python comes pre-installed in Mac. You can check the version of python by using the following command :

> python --version

Download mysql from the http://dev.mysql.com/downloads/mysql/. They have an annoying sign up before download policy that might make you cringe, but just go with it.

Once installed, you start the mysql server in your system preferences.

Most probably, you might notice that the you arent able to launch the command line tools. In that case add /usr/local/mysql/bin to your $PATH in your .bashrc

Set your mysql root password with:

> sudo mysqladmin -u root NEW_PASSWORD 

Next step is to setup a symbolic link for the mysql libraries in /usr/lib with the following command:

> sudo ln -s /usr/local/mysql/lib/libmysqlclient.18.dylib /usr/lib/libmysqlclient.18.dylib

Now download the MySQL library for python from http://sourceforge.net/projects/mysql-python/ . Once you have the file untar it and execute the following commands:

> $ python setup.py build
> $ sudo python setup.py install

During the build you might get a lot of warnings. Its usually safe to ignore the warnings.

The open up python and try importing MySQLdb.

> avallark@Aryan ~/setup/MySQL-python-1.2.4b3 $ python
> Python 2.7.2 (default, Jun 20 2012, 16:23:33) 
> [GCC 4.2.1 Compatible Apple Clang 4.0 (tags/Apple/clang-418.0.60)] on darwin
> Type "help", "copyright", "credits" or "license" for more information.
>>> import MySQLdb
>>> quit()

If you did not receive anything, remember the old unix saying, "No news is good news"!

You are now setup for some python mysql hacking!