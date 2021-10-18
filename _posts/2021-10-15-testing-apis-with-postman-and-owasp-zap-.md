---
layout: post
title: Testings APIs with Postman and OWASP ZAP proxy
description:
headline:
modified: 2021-10-02
category: Testing
tags: [testing, API, postman, ZAP]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

A question came up recently over on the [Ministry of Testing Club Forum](https://club.ministryoftesting.com/t/tool-for-api-and-security-testing/39504/8) where people were sharing thoughts on how you might be able to use a tool for both API and Security Testing.

Whilst I've not used a tool to do both, this got me thinking. Could some of the tools I've used previously be used in combination to achieve this?

I enjoy using [Postman](https://www.postman.com/) to test APIs and have used [OWASP ZAP](https://owasp.org/www-project-zap/) a little. Both tools are free and very easy to get installed and configured and also have some great documentation. ZAP even has some nice [free videos](https://www.zaproxy.org/zap-in-ten/) to help you get started.

Below is a simple way you could choose to test API requests with Postman with ZAP proxy.

### Configuring the tools:


#### ZAP:

* Go to ‘Options’, and click on ‘Local Proxies’
* Ensure the ‘Address’ is set, i.e. localhost
* Ensure ‘Port’ is set, i.e. 12345

#### Postman:
* Go to ‘Settings’ and click on ‘Proxy’
* Scroll down to ‘Proxy configurations for sending requests’ and click on ‘Add a custom proxy configuration’
* Set the ‘Proxy Server’ to localhost, and port to 12345

#### Ready to test:
* Now within Postman you can run individual requests or choose to ‘Run collection’ using Postman’s collection runner. Any alerts that should be investigated will be shown in ZAP along with the URLs/Endpoints called within the ‘Sites’.

##### Issues making requests?
If after configuring both tools and making a request via Postman you see an error within Postman stating “SSL Error: Self signed certificate in certificate chain”, click on ‘Disable SSL Verification’ in order to be able to run the requests and avoid this error. Because the requests are being sent through ZAP (which uses a self-signed SSL certificate) to capture the request and response being sent you might see this error. By default, this certificate is not trusted by your system, browser, or Postman.
You can also go into Postmans ‘Preferences’ and disable ‘SSL certificate verification’ under the ‘General’ tab.

## Why not share your ideas?
I’m sure there are other great tools and ways of achieving what the original poster was asking but this is just one way they could consider. If you have any ideas, why not head over to the [Ministry of Testing Club Forum](https://club.ministryoftesting.com/t/tool-for-api-and-security-testing/39504/8) and share your thoughts?
