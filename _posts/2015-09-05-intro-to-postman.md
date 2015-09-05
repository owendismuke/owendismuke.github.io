---
layout: post
title:  "Intro to Postman"
date:   2015-09-05 14:00:49-7
categories:
- Postman
- API
- testing
comments: true
---

In creating, deploying, and discovering APIs, there is always the need to test that the expected response meets the request sent. To ease this burden, I usually turn to [Postman][postman]. Postman is a tool that let's you try every feature of an API that you can think of a test for. Today's blog is going to cover the basics to get you started.

To start, download [Postman][postman] from the Chrome [web store][postinstall], and run it.  
![Postman]({{ site.url }}/assets/postman_1.png)  

Once loaded, you can perform any number of verbs that you would expect: GET, PUT, POST, OPTIONS. For this blog, we will access the Department of Labor's public API with a GET request, and my application expects the results to be returned in json. Accessing this API requires a mixture of parameters and headers to get the data back in a format that I can use. Luckily, Postman makes these values easy to add, delete, reorder, or update.  
![Options]({{ site.url}}/assets/postman_options.png)  

Now that I've fired off my request and received the response, I am able to view my results, the response code, and the time it took for all of this to complete.  
![Finished]({{ site.url }}/assets/postman_2.png)


[postman]: https://www.getpostman.com/
[postinstall]: https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop