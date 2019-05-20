---
layout: post
title:      "Networking is Knowledge"
date:       2019-05-20 04:55:11 +0000
permalink:  networking_is_knowledge
---



Today I was fortunate enough to meet with the sole developer/IT consultant for an (actual) up and coming start up in the child care / benefits market.  Networking oppurtunities such as these are always way out of my comfort zone but as I begin to challenge myself socially/professionally consistantly I am rewarded with invaluable advice, perspective, and motivation as the arduous journey of transitioning and advancing my career.

After an initial phone call and some minor text logistics I found myself scheduled to meet with a very talented individual in the development field who has the unique experience of running his own IT consulting company while also enjoying the benefits of being a trusted team member in a very valuable yet personal company.  His insights proved to be valuable three fold; I was able to make a face to face connection and opportunity to gain experience working directly with his company, advice on how to start gaining experience on my own, and also a extermely involved lesson on exactly how to launch my own apps/get a server configured using Google Cloud Services.

The lesson on back end configuration was really awesome.  The Flatiron course does a great job of starting at the root of all aspects of web development and working up but although we gain a thorough understanding of what is happening once we launch our servers locally it is much different in a pracatical environment where certain certificates and explicit variables must be set in order to have a functioning app work ona custom domain/url.

We went from cutomizing our own url, to launching a GCS project instance, loaded DNS records for our custom mailing domain and custom url, and configured a app engine instance functioning as a CLI interface for the server actually running our files.  Within each step he was very receptive to my many processes about what exactly was happening at the lowest level in the DNS req/response process.  Specifically interesting and beyond the scope of the course was the concept of records.  Here is the gist:

When the user on their browser enters and submits and uri adress the dns host will use information in that uri to determine which IP adress to send to based on the root domain/subdomains.  It will use this information in reference to a specific "zone" file that an admin can set/configure to root to correct IP address (hopefully) running the right server to process the rest of the uri.  

Before we go into which types of dns requests can be made (more accurately what "records" we can store in the zone file to handle requets) lets talk about what domains/subdomains are.
