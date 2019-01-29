---
layout: post
title:      "fetch is hard, then im frustrated, so im done"
date:       2019-01-06 17:36:45 -0500
permalink:  fetch_http_then_confusion_like_async_functioins_better
---

.fetch("http://then.confusion", {like: "async functions better"})

Async JS really expands our abilities as developers and  allows us to make very complex frontend appplications that are fast and secure by only "posting/fetching" essential data from a secured server operating on a different domain.

The .fetch is the Vanilla JS way of interacting with servers and is itself inherits form the JS  asynchronous function class.

One thing, ide like to preface this all by this is MY understanding of Asynch functions and helps me functionally use async functions in a different way than simply using .then and .catch, so its PROBABLE that i am explaining this technically wrong, I hope you dont mind too much.

So async functions are used by prefaceing a function declaration with "async".   an example would be as follows:

async function asyncCall() {
     // do stuff //
}

Boom, we just declared our async function.  Now we have the ability to use an awesome feature of async funtions, the power to "await".  The MDN explains await as an "expression that pauses the execution of the async function and waits for the passed Promise's resolution, and then resumes the async function's execution and returns the resolved value."

Basically when we preface another async function with "await" code will not parse until a promise has been returned by the nested async function.   This may make more sense using an example and comparing to the .then/.catch methods.

.fetch using .then:

.fecth("hhtp://random-api.com", {data})
  .then(resp => resp.json())
	.then( data => // do something with data // )
	.catch ( err => // retrunan error message // )
	
Using async functionality:

async function getData(data) {
  gettingData = await fecth("hhtp://random-api.com", {data})
	
	if (gettingData.ok?) {
	  // do somethig with gettingData ** response assigned to variable gettingData ** //
	} else {
	  // return an error message //
	}
}

In the asynchronous example we abstract all the functionality of our fetch, then, and catch functinality into a singular named asynchronous function.  This function will "read" very similiar to regular functions and I beleive really helps encapsulate larger more complex fetching capabilities.

A real example where using asynchronous funcitionality over abstracted .then statements is when I was asked by a friend to help returning and displaying tablized data from a server.  The data we were requesting was EXTREMELY large in size, thousands if not ten of thousands of objects and their nested objects were being requested and a singular HTTP request would not handle so much data -- we did try using compression but werent technical enough to find out why it wouldnt work -- so we used instead a paginated request / response format and it worked well.  My friend was handlng the back end but basically would paginate the date (breaking it into smaller, manageable chunks, and able to be requested individually), so instead of requesting /items we would request first to /items/1 and handle a response of the first 1000 or so items and then requests made to /items/2 would be the next 1000 or so responses and so on until there wasnt any more items left in the data base.  With the backend succesfully handling requests with this logic I used the following code to handle retriving all items in a singular function (credit to stack overflow for the base functionality and starting me on the path of async functions):

    getStuff = async () => {

        var pages = 1;
        var responses = []
        while(true) {
    
            var res = await fetch(`${window.location.origin}/api/items/${pages}`);
    
            if(!res.ok) break
    
            var data = await res.json();

            responses = [...responses, data]

            pages += 1
    
        };
        this.setState({
            items: responses.flat(),
        })
    };
		
So breaking this response down a bit we basically declare variables as a page index and an empty array container for our response items to be collected and stored as we cycle through responses.  The next phase is really cool and basiically a while(true) {} loop will initiate an infinite loop.  Inside this self-made inifinite loop we make an insitial request (while loops always fire atleast once) and than we proceed to process the response (if it is ok? (successful) or than we break the infinite loop if the repsonse errors.  Ending with us doing some React stuff to display the data.


