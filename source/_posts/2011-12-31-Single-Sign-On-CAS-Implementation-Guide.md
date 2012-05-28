---
layout: post
title: Single Sign On - CAS Implementation Guide
comments: true
categories: work, product manager, architect, IT strategy
---

 The capability of single sign on seems to be a very basic infrastructural requireme for any organisation, yet the number of companies without a functioning sso is amazingly high.

IESE for instance is one of them. So the first thing I did whe I accepted this job is to initiate a single sign on project. Implementing an SSO brings with it some additional challenge.

* Why Single Sign On
* Directory services
* Application Design to use CAS
* User Management
* Inventorying the applications that must do SSO.
> Which users within the aplications should use SSO and  what mode of authentication is best: Web, Kerberos or Direct authentication.
* Product selection
* Preparing infrastructure
* Building a failsafe system.
* Design
* Integrating applications.

I will go through each of these steps that we followed and why?

## Why Single Sign On

*Before SSO* the user experience within your organization looks somewhat like this.

![Multiple logins and multiple accounts](/work/cas/BeforeSSO.png "Before SSO")

*After SSO* the user experience _could possibly_ be something like this.

![Single login and one time entry](/work/cas/AfterSSO.png "After SSO")

## Directory Services and Identity management

We use active directory. Our University "Universidad de Navarra" uses OpenLDAP. We had to do single sign on between both our school and the University. CAS has in-built support for both. Specify within the Server xml which beans and the server details like ldap.expample.com, its port and a non-anonymous service login to bind for the search. 

Most of the time, based on your directory service configuration you will be able to specify clusters of users to authenticate with particular branches of your directory server. This is recommended as it speeds up authentication process for CAS. for e.g. If you have all your students with the email : student@alumni.school.edu, and have your LDAP with a sub branch called students where all your students exist, then its a good idea to create a separate alumni LDAP server (even if its based on the same LDAP server as staff) just for students. This student's ldap server item on your xml will instruct CAS to do search on the sub-branch of "DC=students,DC=iese,DC=edu".

An example of the server configuration file is [available here](http://github.com/avallark/avallark.github.com/projects/cas/server.xml)

## Application design to use CAS

One thing to understand is that CAS provides authenticaton. You can configure it such that it will return a few LDAP attributes like email id, username etc. CAS also retains the user session so as to provide a single sign on experience. The scope ends there. Application designers have come to me with extremely weird requirements from the SSO because they were able to get all these information and access details directly from the Active Directory. This is not why CAS was made. CAS was made as your first door to the application. The apications that are going to use CAS need to follow this design.

![Application design to use CAS](/work/cas/AppDesignCAS.png  "Application design to use CAS")

The application if it wants more user information, needs to have a service account in your LDAP with read-rights over the respective user accounts. 

Once the user has logged in to the application using CAS now the application can safely connect to the LDAP with the service user account and get more information and decide what to do with the user.

This should cover the basic application design. Now you need to decide how you want to integrate the application with CAS. This fairly depends on the kind of application in itself. We here are integrating only web-based applications only. More or less most of our applications are web-based so it suits us well.

For Web based applications, the options are to use SAML. The application you use must support this structure. CAS (current version 3.3.4) supports SAML 1.1. Google Apps uses SAML to authenticate. SAML requires CAS to return an XML structure with the username back to the application. The application then deciphers this structure and unlocks it using the certificate of the CAS server that is installed in the application to read the username. Some applications can request for extra parameters from SAML. This could be done by adding a SAML bean for the particular application. 

The modification for google apps is [given here](https://wiki.jasig.org/display/CASUM/SAML+2.0+%28Google+Accounts+Integration%29).

Other forms of integrations include client integration using PHP,.NET, Java or Python.

### Using PHP

Using PHP, the supported client is [PHPCas](https://wiki.jasig.org/display/CASC/phpCAS) (current version 1.2.2). The installation is explained there, but you might find the below explaination easier.

Download PHPCas to a directory that can be accessed by the PHP page. Copy the certificate of the server x509.pem and save it to a directory cert_directory within reach. Also create a db schema (if required). 

Edit your application php file to include the following.
	 
	include_once('cas/config.php');
	include_once($phpcas_path.'/CAS.php');
	phpCAS::setDebug();
	phpCAS::client(CAS_VERSION_2_0, $cas_host, $cas_port, $cas_context);
	phpCAS::setNoCasServerValidation();
	phpCAS::forceAuthentication();
	if (isset($_REQUEST['logout'])) {
        phpCAS::logout();
	}
	if (phpCAS::isAuthenticated()) {
		$name = phpCAS::getUser(); //This is the variable that has the name. 
		// You could use this further in your program.
	// And the program can continue for authenticated users with $name.
	

Use the config.php file that we included (the file can be found within PHPCas directory under examples) and add in the configuration details like host, db etc.

If your CAS url is something like : https://login.example.com/cas

	$cas_host = 'login.example.com'
	$cas_context = '/cas';
	$cas_port = 443; // This will be the port of the initial server, not the catalina port.
	$cas_server_ca_cert_path = '/path/to/cert_directory/x509.pem';
	$db = 'mysql:host=localhost;dbname=<dbname>';
	$db_user = 
	$db_password = 
	$db_table = 


Then go to your application php and it will redirect you to CAS for Authentication.

You could find more examples and other client integrations on the [CAS wiki](http://www.jasig.org/cas/client-integration).

To get more information from the LDAP now you can use this $name to query information. An example is given below (Will be updated)

## User Management

One of the things to consider while integrating your application with Single Sign On is the which users of the applications need the single sign on. Usually organizations get so lost in the frantic single-sign-on-paranoia that they issue mandates to application teams to integrate all users with SSO in all cases. 

The general rule of thumb policy to follow would be to give your *customers* a single sign on. Administration & staff can use special administrative logins and letting them login multiple times is not an issue. SSO should be for your customers. So when the customer clicks on the login button of your website, take them to the SSO. Have a separate url (like example.com/admin/) for the admin and staff logins. This also makes it easier for application developers to have a separate area for admin & staff.

