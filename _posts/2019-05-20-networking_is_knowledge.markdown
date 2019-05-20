---
layout: post
title:      "Networking is Knowledge"
date:       2019-05-20 00:55:12 -0400
permalink:  networking_is_knowledge
---



Today I was fortunate enough to meet with the sole developer/IT consultant for an (actual) up and coming start up in the child care / benefits market.  Networking oppurtunities such as these are always way out of my comfort zone but as I begin to challenge myself socially/professionally consistantly I am rewarded with invaluable advice, perspective, and motivation as the arduous journey of transitioning and advancing my career.

After an initial phone call and some minor text logistics I found myself scheduled to meet with a very talented individual in the development field who has the unique experience of running his own IT consulting company while also enjoying the benefits of being a trusted team member in a very valuable yet personal company.  His insights proved to be valuable three fold; I was able to make a face to face connection and opportunity to gain experience working directly with his company, advice on how to start gaining experience on my own, and also a extermely involved lesson on exactly how to launch my own apps/get a server configured using Google Cloud Services.

The lesson on back end configuration was really awesome.  The Flatiron course does a great job of starting at the root of all aspects of web development and working up but although we gain a thorough understanding of what is happening once we launch our servers locally it is much different in a pracatical environment where certain certificates and explicit variables must be set in order to have a functioning app work ona custom domain/url.

We went from cutomizing our own url, to launching a GCS project instance, loaded DNS records for our custom mailing domain and custom url, and configured a app engine instance functioning as a CLI interface for the server actually running our files.  Within each step he was very receptive to my many processes about what exactly was happening at the lowest level in the DNS req/response process.  Specifically interesting and beyond the scope of the course was the concept of records.  Here is the gist:

When the user on their browser enters and submits and uri adress the dns host will use information in that uri to determine which IP adress to send to based on the root domain/subdomains.  It will use this information in reference to a specific "zone" file that an admin can set/configure to root to correct IP address (hopefully) running the right server to process the rest of the uri.  

Before we go into which types of dns requests can be made (more accurately what "records" we can store in the zone file to handle requets) lets talk about what domains/subdomains.  A domain is the "root" of your uri.  "Example.com"'s domain would be "example.com".  A subdomain would be what proceeds the domain.  "test.example.com" would have a subdomain of "test".  We can set where to map our root domain using the "@" symbol and we can create subdomains as texts pointing to whichever server IP we would like as well.  We can set a domains and subsequent subdomains to the same IP. 

Now different records will illicit different response types by where/how we delcare the associations.  A records (and AAAA records in ip6) are the most traditional DNS routing record.  They map domains and subdomains to an IP adress creating a host association, where a custom domain will host a specified IP running on your server.  These hosts associations are used later in the other types of records.

CNAMES are used almost as "namespaces".  If we wanted to created a new subdomain strcitly for namesake we can use CNAMES to point to a host association rather than an new IP address.  Using our above example once the test.example host was set up we can than use demo.example.com to point to that same host rather than create a new one.  This functionality is used two fold.  In todays web the "www." is no longer not just not required but will mess up how DNS requests are handled (looking for a cname or a subdomain).  In order to compensate we can create a "www." cname to point to the domain (i.e. root not subdomain) host and functionality resumes seamlessly to end user.  Furthermore if we wanted to redirect the user to another user without disrupting the current URI we can use the same cname technique, for example if we could have "redirect_to_other_host_not_shown.example.com" point to a completely different domain host than example.com "not_example_domain.com".

Another type of request is the MX request which is used to facilitate email exchange to domain/subdomain.  Here established A record hosts can be pointed to when referencing our custom domain.  This seperate record recieves a priority level as well as subdomain names.
