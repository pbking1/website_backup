---
layout: post
title: "linkedin_api_example"
date: 2015-02-12 14:51:14 -0500
comments: true
categories: api python
---

- we can use the RESTFUL api to get some information in linkedin
	- https://apigee.com/console/linkedin
		- this is a online simluator to perform RESTFUL api of linkedin
<!--more-->
- and the sample code below is using the linkedin package from thrid party 
	- you can download the package using the following link
		- https://pypi.python.org/pypi/python-linkedin/4.0
		- https://github.com/ozgur/python-linkedin
- code
	- the following code can produce some result
		- but I have some problem in using the search api
			- application.search_profile(selectors=[{'people': ['first-name', 'last-name']}], params={'keywords': 'apple microsoft'})
		- Search URL is 'https://api.linkedin.com/v1/people-search:(people:(first-name,last-name))?keywords=apple%20microsoft'
		
```
#! /usr/bin/env python
# -*- coding: utf-8 -*-

CONSUMER_KEY = 'xxxxxxx'     # This is api_key
CONSUMER_SECRET = 'xxxxxxx'   # This is secret_key

USER_TOKEN = 'xxxxxxx'   # This is oauth_token
USER_SECRET = 'xxxxxxx'   # This is oauth_secret
RETURN_URL = 'http://localhost:8000'

from linkedin import linkedin
from oauthlib import *
from urllib2 import *
import urllib2
from json import dumps, loads
# Define CONSUMER_KEY, CONSUMER_SECRET,  
# USER_TOKEN, and USER_SECRET from the credentials 
# provided in your LinkedIn application

# Instantiate the developer authentication class
authentication = linkedin.LinkedInDeveloperAuthentication(CONSUMER_KEY, CONSUMER_SECRET, 
                                                      USER_TOKEN, USER_SECRET, 
                                                      RETURN_URL, linkedin.PERMISSIONS.enums.values())

# Pass it in to the app...
application = linkedin.LinkedInApplication(authentication)

print application.get_profile()

print application.get_profile(selectors=['id', 'first-name', 'last-name', 'location', 'distance', 'num-connections', 'skills', 'educations'])

print application.search_company(selectors=[{'companies': ['name', 'universal-name', 'website-url']}], params={'keywords': 'apple microsoft'})
# Search URL is https://api.linkedin.com/v1/company-search:(companies:(name,universal-name,webs

print application.get_memberships(params={'count': 20})

print application.get_companies(company_ids=[1035], universal_names=['apple'], selectors=['name'], params={'is-company-admin': 'true'})

```
