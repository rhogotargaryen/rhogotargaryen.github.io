---
layout: post
title:      "class CLI_proj"
date:       2018-02-21 00:35:33 +0000
permalink:  class_cli_proj
---


  This was/is definitely a big undertaking for me and a lot of information learned over the past few weeks definitely came to a head.  Timing perfectly imperfectly with my atypical and not very scheduled work schedule it was very difficult to get up and going and undertake the arduous task of consolidating a lot of information.
  My first big struggle was with setting up a non-learn dev environment.  I opted to use the cloud9 AWS service and mosly my fault for not completely following the tutorials (its 2 pages!!) it took me a half days effort to get it set up correctly and then another half day to learn/connect my account withgithub.  After a lot of effort and asking questions I finally was redirected to the tutorial which did a great job of thoroughly setting up a cloud DE and I dont regret my time fully understanding the process.  Great job to the Flatiron team on the tutorial tho.
	Once up and running with an dev environment it was time to configure/bundle my gem to actually begin making the CLI app.  This took a while to master and through trial and error i was able to establish a working environment file as well as a console for testing.  Configuring the environment file was difficult and but helped me understand a little bit more about how files interact with each other.  Also it was fun adding gems to the gemspec, tho i didnt really use many (at all) specifications in them.  Hopefully when testing with other students it wont become a problem.  I ran into some trouble with openURI that snagged me for a while and had me asking questions everywhere I could.   In the end I was confused about not needing to require the gem since it was native to ruby and I look forwarding to knowing this for any future issues.
	As of right now I have a working(ish) app without a CLIcontroller.  Im struggling a bit becase my scraper class has basically become my OBJ class and im not sure if or why I should construct a seperate class just to hold information already parsed but also want to demonstrate an ability to interact with objects.  Also I would like to add some color to my app which will take some time.
	I guess I should explain my app...  It is a DC/Marvel superhero information gatherer.  You can enter a name in really any format thE iRON mAn", "Iron Man", or "the iron man" and it will parse wether there is a match to a website.  It will turn that name into a parameter as a url ending and then parse that hero's website for its information.  The open-sourceness of the website really hampers my ability to parse individual pieces of data so in testing I found that simply returning all the paragraphs within a certain wrapper will return data in a fairly elogant way although larger more popular heroes have often more text than most others.
  I am excited to head to a study group, office hours, and hopefully a 1 on 1 on my way to making a polished app.  thank you for reading!
	
	end
	
