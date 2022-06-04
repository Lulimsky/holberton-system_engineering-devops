# 0x19. Postmortem

## Description
Any software system will eventually fail, and that failure can come stem from a wide range of possible factors: bugs, traffic spikes, security issues, hardware failures, natural disasters, human error… Failing is normal and failing is actually a great opportunity to learn and improve. Any great Software Engineer must learn from his/her mistakes to make sure that they won’t happen again. Failing is fine, but failing twice because of the same issue is not.

A postmortem is a tool widely used in the tech industry. After any outage, the team(s) in charge of the system will write a summary that has 2 main goals:

To provide the rest of the company’s employees easy access to information detailing the cause of the outage. Often outages can have a huge impact on a company, so managers and executives have to understand what happened and how it will impact their work.
And to ensure that the root cause(s) of the outage has been discovered and that measures are taken to make sure it will be fixed.

![](https://i.redd.it/vri4ra46xi531.jpg)

 ## Handling API Gateway 500 Error: Internal Server Error
 
The 500 status code might be the most used and most generic HTTP error on this planet. If you get it from an API endpoint that integrates with AWS Lambda, it usually means your code buggy.

The next source for this error is inconsistent error mapping. Many of the errors we talked about here can become a 500 error when finally landing on your client as a response. You’ll get a “limit exceeded,” but it will have a 500 status code instead of 429. So you have to extract the right error out of this response, check what the real cause is, and then look at how to solve it.

Since the error can be anything really, a retry can technically solve that problem, but usually, it doesn’t.

If you monitor your system carefully and get one of these every few million requests, it could be that cosmic rays flipped some bits or whatever. Still, if you see a 500 status code more often than that, it’s crucial to investigate; it can very well point to an inconsistency that will blow up sooner or later.

So here is the postmortem report on debbuging an 500 Error:  https://docs.google.com/document/d/1Q67BoQ3Y0dm-r6jnCPwnD-_Vqf-9wZYTABahYgzuTuE/edit?usp=sharing
