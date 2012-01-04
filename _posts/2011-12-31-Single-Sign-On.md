---
layout: post
title: Single Sign On - Implementation Guide
author: Abdul Bijur Vallarkodath
---

# Single Sign On - CAS Implementation Guide

 The capability of single sign on seems to be a very basic infrastructural requireme for any organisation, yet the number of companies without a functioning sso is amazingly high.

IESE for instance is one of them. So the first thing I did whe I accepted this job is to initiate a single sign on project. Implementing an SSO brings with it some additional challenge.

* Why Single Sign On
* Directory services
* Access management processes
* User classification
* Identifying the different organisations within which the authentication must happen
* Inventorying the applications that must do SSO.

Which users within the aplications should use SSO and  what mode of authentication is best: Web, Kerberos or Direct authentication.

* Product selection
* Preparing infrastructure
* Building a failsafe system.
* Design
* Integrating applications.

I will go through each of these steps that we followed and why?

## Why Single Sign On

.. Google docs presentation..

## Directory Services and Identity management

We use active directory. Our University "Universidad de Navarra" uses OpenLDAP. We had to do single sign on between both our school and the University. CAS has in-built support for both. Specify within the Server xml which beans and the server details like ldap.expample.com, its port and a non-anonymous service login to bind for the search. 

Most of the time, based on your directory service configuration you will be able to specify clusters of users to authenticate with particular branches of your directory server. This is recommended as it speeds up authentication process for CAS. for e.g. If you have all your students with the email : student@alumni.school.edu, and have your LDAP with a sub branch called students where all your students exist, then its a good idea to create a separate alumni LDAP server (even if its based on the same LDAP server as staff) just for students. This student's ldap server item on your xml will instruct CAS to do search on the sub-branch of "DC=students,DC=iese,DC=edu".

An example of the server configuration file is [available here](http://github.com/avallark/avallark.github.com/projects/cas/server.xml)

## Application design to use CAS

One thing to understand is that CAS provides authenticaton. You can configure it such that it will return a few LDAP attributes like email id, username etc. CAS also retains the user session so as to provide a single sign on experience. The scope ends there. Application designers have come to me with extremely weird requirements from the SSO because they were able to get all these information and access details directly from the Active Directory. This is not why CAS was made. CAS was made as your first door to the application. The apications that are going to use CAS need to follow this design.

Img

The application if it wants more user information, needs to have a service account in your LDAP with read-rights over the respective user accounts. 

Once the user has logged in to the application using CAS now the application can safely connect to the LDAP with the service user account and get more information and decide what to do with the user.