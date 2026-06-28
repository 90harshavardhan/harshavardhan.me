---
title: Proxy Servers
author: Harsha Vardhan
date: 2018-12-01T10:25:06+00:00
draft: true
categories:
  - system-design-architecture
  - system-performance-scalability
tags:
  - anonymous proxy
  - forwarding proxy
  - open proxy
  - proxy server
  - reverse proxy
  - transparent proxy

---
A proxy server is a process that acts as an intermediary for requests from clients seeking resources from other servers. A proxy server can be a dedicated computer system for the job or merely an application running on a system along with other tasks performed by the system. Sometimes it can be a process running on the client system as well.

Other than one basic established fact that they exist to ensure that request and response passes through them there is no strict guideline on the roles or activities they may perform. Their job can be a mix of many activities/categories described below.

If it may help Proxy Servers can be considered as an employee of an company with mixed set of responsibilities of a receptionist, as intercom call router, security personal at gate, an access card swipe machine which needs card to be swiped every-time someone passes through a door. We can broadly classify them in following categories:

#### 1. Gateway (or tunnelling) proxy:

They pass requests and responses unmodified. They are used as protocol translators, impedance matching devices, rate converters, fault isolators, firewalls or signal translators.

#### 2. Forward proxy:

It is an Internet-facing proxy used to retrieve data from a wide range of sources. This can be further classified in two categories:

##### 2.1 Anonymous Proxy –

Thіs type of server reveаls іts іdentіty аs а server but does not dіsclose the іnіtіаl IP аddress. It allows users to conceal their IP address while browsing the Web or using other Internet services. This is like a security personal allows you to go in and walk out without asking for your ID card(I think, this guys is like a Church security guy who doesn&#8217;t care who you are). How else had you been browsing websites(e.g. Facebook etc) from your school/college computer which were blocked by Firewalls.

##### 2.2 Trаnspаrent Proxy –

Thіs type of proxy server аgаіn іdentіfіes іtself, аnd wіth the support of HTTP heаders, the fіrst IP аddress cаn be vіewed. The mаіn benefіt of usіng thіs sort of server іs іts аbіlіty to cаche the websіtes. Sometіmes, your IP mаy get bаnned аs а result of the use of trаnspаrent proxy. Your Internet Protocol аddress іs not hіdden іn thіs server.

#### 3. Reverse Proxy:

This is an interesting one. As it exists to help or protect and internal network of hosts. Reverse proxies forward requests to one or more ordinary servers which handle the request. The response from the proxy server is returned as if it came directly from the original server, leaving the client with no knowledge of the origin servers. Reverse proxies are installed in the neighbourhood of one or more web/application servers.<figure id="attachment_364" aria-describedby="caption-attachment-364" style="width: 220px" class="wp-caption aligncenter">

<img loading="lazy" decoding="async" class="wp-image-364 size-full" src="/wp-content/uploads/2018/12/220px-Reverse_proxy_h2g2bob.svg_.png" alt="Reverse Proxy" width="220" height="83" /> <figcaption id="caption-attachment-364" class="wp-caption-text">Reverse Proxy</figcaption></figure> 

  * Load balancing: It can distribute the load to several web servers, each web server serving its own application area.
  * Collapsed forwarding: When coordinating requests from multiple servers and can be used to optimize request traffic from a system-wide perspective. We can collapse the same (or similar) data access requests into one request and then return the single result to the user.
  * Static Caching: It can offload the web servers by caching static content like pictures and other static graphical content.
  * Compression: Optimize and compress the content to speed up the load time.
  * Encryption / SSL acceleration: A host can provide a single &#8220;SSL proxy&#8221; to provide SSL encryption for an arbitrary number of hosts; removing the need for a separate SSL Server Certificate for each host.

_**Further thoughts:**_ Another great way to use the proxy is to collapse requests for data that is spatially close together in the storage (consecutively on disk). This strategy will result in decreasing request latency. If a bunch of servers request parts of file. We can set up our proxy in such a way that it can recognize the spatial locality of the individual requests, thus collapsing them into a single request and reading complete file, which will greatly minimize the reads from the data origin.