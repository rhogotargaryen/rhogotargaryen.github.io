---
layout: post
title:      "Javascipt lessons learned a long the way"
date:       2018-08-24 01:45:06 -0400
permalink:  things_learned_through_jquery_project
---

	
	
	
Hello and thank you for taking the time to read my latest blog post.  Learning Javascript has been a lot of fun and learning how to interact with the DOM and the SERVER using jquery and JSON requests has made me really feel to some degree like an actual developer.  The enthusiam to learn has lead to a lot of trial and error especially when refreactoring a JQUERY front end to my rails project.  Through the tension of putting out one fire only to extinguish another I have learned some really helpful things about JS, JQUERY, and AJAX that would be valuable to those starting their projects with some understanding of the basic patterns taught in the curriculum.
	
I think the first major thing I learned is that JS, AJAX, and JQUERY essentially all do the same things, it can even be thought of as levels of abstractions on top of each other.  I personally found using JQUERY very effective at getting most if not all of what I needed to get done .  it  like JQUERY abstracts a lot of the configuration out of JS and AJAX and I have found to be an all-in-one tool for selecting elelements, adding listeners, making server requests, and manipulating the DOM.  At the least using it as shorthand for document.ready() ($()) and document.getElementBy(id, class, etc) ("") worth using JQUERY alone	
	
Once pretty well practiced in selecting DOM elements and sending proper requests and responses from the server learning how to attach listeners and manipulate DOM elemenents correctly became my new challenges.  From them however I learned several great practices and would like to share!
		
Before talking about attaching event listeners properly lets talk about DOM manipulation and a situation where needing to know a little more about JS will help us understand and code a more effective solution.   Let us say that we have a button "create new item form" that when clicked will add a form element to the DOM and removes itself with a new button "remove new item form" which will perform its namesake as well as add back the create new item button.
		
It would seem intuitive how to perform this, we would listen for a click on the #create_form_button and on click we would send a request for our new item form html and than append it to the DOM element of our liking.  Next we could select the #create_button again and remove it, change its html contents to "". etc.  The issue would be when firing the #remove_form_button.  One would think that you could simply append back an element syntatically equal to the #create_form_button we had removed earlier and simply append it back into the dom, even nested exactly where it used to.  We would quickly and furiously find out that this would not work.  Although the button resides and has the same html code as the one we previously removed the JS of that code will not fire.  It seems though that document ready fired once, on screen load and does not do so again everytime a new element is added. 
		
 In order to fix this we have to use a specific attach/detach pattern.  When using attach/detach we preserve the JS functionality of the dom element even tho it has been "detached" or visibly removed from the DOM.  to (re) attach an element back to the DOM with its preserved JS functionality we first need to set our original deatching of an element to a variable).  so if we used var a = $('#create_form_button').detach().  $('#create_form_button') would be removed ffrom the DOM, a would now store the HTML of the create button, and remain in the scope of our JS code fired on document.ready.  so if later perhaps on the remove_form_button click event we can then use the following code.  
$('#some_container').attach(a).  This would make our original #create_form_button appear with the same listeners and code we attached to it originally.

 Hopefully the above will help when adding and removing DOM elements that were present at document.ready().  Lets dig deeper into our example situation and explore how we can use event listeners at document.ready() that will be able to add AJAX functionality to elements added to the dom without being present at the initial document.ready() script firing.
	
 An example might make things more clear.  Ok so lets say our #create and #remove_for_buttons work properly and we succusffuly add and remove a new item form to our DOM.  Now we would like to select and "hijack" the actual #create_item_button to post a request to our server and handle the json response.  One would think it would be simple as adding an event listener for #create_item_button on our initial document.ready script and all would be well.  WRONG.  We run into the same issue where since that element was not presenet at document ready there was no element present to select.  In order to have functionality added to that element we have to add the event listener to a parent element in the DOM.  So if we were to have our form added to empty div that already was present at document load, we can attach a submit listener to that element that will fire when clicked.

