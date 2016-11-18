#Python#

##Education##
1. [The Hitchhiker's Guide to Python](http://docs.python-guide.org/en/latest/)
2. https://developers.google.com/edu/python
3. https://wiki.python.org/

##Tools##
1. [PIP tool for installing and managing Python packages.](https://pip.pypa.io/en/latest/index.html)
2. [VirtualEnv](http://docs.python-guide.org/en/latest/dev/virtualenvs/)
3. [Wingide101](http://wingware.com/downloads/wingide-101)

## Templates ##
1. [Templates Overview](https://wiki.python.org/moin/Templating)
2. General Templates:
   - [Mustache](http://mustache.github.io/) - a trivial template not only for Python.

## Install ##

### Python 3.5 at RHEL 7 ###

1. Remove existing (or similar) installation
   `yum remove python34-libs-3.4.3-7.el7 python34`
2. Install Python 3.5
   Useful article on that can be [found here][1].  
   `yum install -y https://centos7.iuscommunity.org/ius-release.rpm`  
   `yum install -y python35u python35u-pip python35u-devel`  

   The `virtualenv` might be also useful later, so let's install it now:  
   `pip3.5 install virtualenv`  
   `pip3.5 install pbr`  
   `pip3.5 install virtualenvwrapper`  

3. Install Oracle 12c libraries
   [Source][2].

   `echo $ORACLE_HOME/lib >> /etc/ld.so.conf.d/oracle.conf`  
   `ldconfig`  

   I encountered some issues with broken pip3.5 after Oracle  
   has been installed. It has been mentioned [here][issue1].  
   `export ORACLE_HOME=/opt/oracle/product/11.2.0/dbhome_1`  

   `cd $ORACLE_HOME/lib/`  
   `mv libexpat.so libexpat.NOF`  
   `ldconfig`  

   `yum install libaio`  
   `rpm -Uvh oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm`  
   `rpm -Uvh oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm`  
   `rpm -Uvh oracle-instantclient12.1-sqlplus-12.1.0.2.0-1.x86_64.rpm`  

4. Now install cx_Oracle
   `pip3.5 install cx_Oracle`

## WWW ##

### WWW Templates ###

1. Light Solutions
   - [Jinja](http://jinja.pocoo.org/) full featured template system for Python
   - [Jinja Example](http://runnable.com/Upjr1LZv_TADAAOj/example-website-layout-in-jinja2-for-python-and-wsgi)
   - [Flask](http://flask.pocoo.org) 
2. [Google Cloud - Using Templates](https://cloud.google.com/appengine/docs/python/gettingstartedpython27/templates)
3. [Apache's mod_wsgi](http://flask.pocoo.org/docs/0.10/deploying/mod_wsgi/)
4. [Tornado](http://www.tornadoweb.org/en/stable/) Python web framework

### django ###
Django is not only about templates. It deserves a dedicated section.

1. [Tutorial](https://docs.djangoproject.com/en/1.7/intro/tutorial01/)
2. [Tutorial Files](https://github.com/django/djangoproject.com)


[1]: http://stackoverflow.com/questions/8087184/problems-installing-python3-on-rhel
[2]: https://www.mylinuxplace.com/install-cx_oracle-on-centos-7/
[issue1]: https://bbs.archlinux.org/viewtopic.php?id=140916
