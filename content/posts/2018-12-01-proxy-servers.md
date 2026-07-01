---
title: Proxy Servers
author: Harsha Vardhan
date: 2026-07-01T10:51:00+00:00
draft: true
slug: proxy-servers
categories:
  - technology
tags:
  - anonymous proxy
  - forwarding proxy
  - open proxy
  - proxy server
  - reverse proxy
  - transparent proxy
---

We often hear the term **proxy** — in tech conversations, in network 
settings, in VPN apps. But here's a fun fact: long before our introduction 
to computer systems, most of us used this word since school. When a present 
fellow student responded "here" on behalf of a missing classmate during 
attendance, we said he *marked proxy*. Simple, relatable, and slightly 
illegal 😄.

<figure>
<img src="/wp-content/uploads/2026/07/proxy_attendance.png" 
alt="Classroom attendance proxy" 
style="display:block;margin:0 auto;max-width:100%;"/>
<figcaption style="text-align:center;">The original proxy — marking attendance for an absent friend</figcaption>
</figure>

## What is a Proxy?

In plain English — a proxy is someone or something that acts on your behalf, 
sitting in between you and whoever you're trying to reach. You never directly 
interact with the other side — everything goes through the proxy.

A few more real-life examples you may recognize:

- **Secretary / Personal Assistant** — calls come in for the boss, the 
  secretary takes the message, consults the boss, and responds back. The 
  caller never directly reaches the boss. *(Reverse Proxy)*
- **Lawyer in court** — the lawyer speaks on behalf of the client. The judge 
  never directly addresses the client. *(Forward Proxy)*
- **Real estate broker** — buyer and seller never directly negotiate. The 
  broker carries messages both ways. *(Can be either)*
- **VPN service** — your device connects to a VPN server, which connects to 
  the website on your behalf. The website only sees the VPN's IP, not yours. 
  *(Forward Proxy)*

> *In a dictionary:* Proxy — "the authority to represent someone else, 
> or a person authorized to act on behalf of another."

## Proxy Servers — How Does This Apply to Computer Systems?

In computer networks, a proxy server works exactly the same way as our 
real-life examples — it sits between a client (your browser, app, or device) 
and a server (a website, API, or database). The client sends its request to 
the proxy, the proxy forwards it to the server, gets the response, and sends 
it back to the client. The client and server never directly communicate.

### How are proxy servers classified?

There is no canonical, standards-body list. In practice, technical literature 
classifies proxies along six recurring axes, with rotation behavior often 
treated as a seventh:

1. **By traffic direction** — forward vs. reverse
2. **By anonymity level** — transparent, anonymous/distorting, elite
3. **By protocol / OSI layer** — HTTP, HTTPS/SSL, SOCKS (4/5), plus the 
   L4 vs. L7 distinction
4. **By IP source** — datacenter, residential, mobile, ISP/static-residential
5. **By service / function** — caching, gateway, content-filter, load 
   balancer, API gateway, CDN, SMTP, DNS, SIP, etc.
6. **By access model** — public/open, shared, dedicated/private
7. **By rotation behavior** — static, rotating, sticky-session

A real-world proxy is typically described by picking one value from each 
axis — for example, "an elite, rotating, residential, SOCKS5 forward proxy" 
is one thing described across four axes simultaneously.

### The authoritative standard — RFC 9110

The most authoritative anchor comes from RFC 9110 (the current HTTP 
standard), which defines exactly three forms of HTTP intermediary in §3.7:

> *"There are three common forms of HTTP 'intermediary': proxy, gateway, 
> and tunnel."*

- **Proxy** — "a message-forwarding agent that is chosen by the client, 
  usually via local configuration rules." This is what we call a 
  **forward proxy** — the client knowingly routes traffic through it.

- **Gateway (reverse proxy)** — "an intermediary that acts as an origin 
  server for the outbound connection but translates received requests and 
  forwards them inbound to another server or servers." The client has no 
  knowledge of what lies behind the gateway.

- **Tunnel** — "acts as a blind relay between two connections without 
  changing the messages." A tunnel passes bytes completely unmodified — 
  the classic example is when a forward proxy handles HTTPS traffic via 
  the HTTP `CONNECT` method.

Everything else in the industry vocabulary — load balancers, API gateways, 
CDNs, anonymous proxies, SOCKS proxies — is a refinement of these three.


<figure>
<img src="/wp-content/uploads/2026/07/forward_reverse_proxy.png" 
alt="Forward and Reverse Proxy diagram" 
style="display:block;margin:0 auto;max-width:100%;"/>
<figcaption style="text-align:center;">Forward and Reverse Proxy — Generated using OpenAI gpt-image-2</figcaption>
</figure>

## Forward Proxy

A forward proxy is chosen by the client and sits between the client and 
the internet. The client is fully aware it is using a proxy — it 
intentionally routes its requests through it. The server on the other end 
sees the proxy's IP, not the client's.

**Common uses:**
- **Anonymity** — hiding the client's real IP address from the destination 
  server
- **Content filtering** — corporate networks and schools use forward proxies 
  to block access to certain websites
- **Caching** — repeated requests for the same resource are served from 
  the proxy's cache, saving bandwidth
- **Bypassing geo-restrictions** — accessing content that is blocked in 
  the client's region by routing through a proxy in a different location

**Types of forward proxy by anonymity level:**

- **Transparent proxy** — identifies itself as a proxy and passes the 
  client's real IP via HTTP headers. The client may not even know it is 
  being proxied. Used mainly for caching and content filtering, not 
  anonymity.

- **Anonymous proxy** — hides the client's real IP but still signals that 
  a proxy is being used (via the `Via` header). The server knows a proxy 
  is involved but not who the real client is. Remember accessing websites 
  blocked by your school or college firewall? That was likely an anonymous 
  proxy at work.

- **Elite / High-anonymity proxy** — strips all identifying headers so the 
  request appears to be a direct connection. The server has no idea a proxy 
  is involved. The strongest anonymity level — used by VPNs and tools like 
  Tor.

**Note:** These anonymity tiers apply only to HTTP proxies. SOCKS proxies 
operate at a lower network layer and don't insert HTTP headers at all — 
making SOCKS5 inherently more anonymous than HTTP-level proxies for many 
use cases.

---

## Reverse Proxy (Gateway)

A reverse proxy sits in front of servers, not clients. The client has no 
idea it is talking to a proxy — it believes it is communicating directly 
with the origin server. The reverse proxy accepts requests, forwards them 
to one or more backend servers, and returns the response as if it came 
from itself.

**Common uses:**
- **Load balancing** — distributes incoming traffic across multiple backend 
  servers, ensuring no single server is overwhelmed
- **Collapsed forwarding** — when multiple clients request the same data, 
  the proxy collapses them into a single upstream request and returns the 
  result to all waiting clients — reducing load on the origin server
- **Static caching** — offloads servers by caching static content like 
  images and CSS files, serving them directly without hitting the origin
- **Compression** — compresses responses before sending to clients, 
  speeding up load times
- **SSL/TLS termination** — handles SSL termination for multiple backend 
  servers, removing the need for individual SSL certificates on each server
- **Protocol translation** — bridges between different protocols or 
  network systems

**The reverse proxy family** — in modern infrastructure, reverse proxies 
have evolved into several specialized forms:

- **Load Balancer** — focuses purely on distributing traffic across a 
  backend pool, operating at L4 (TCP/UDP) or L7 (HTTP-aware routing)
- **API Gateway** — adds authentication, rate limiting, quotas, request 
  validation, and analytics on top of routing; the right default for 
  microservices architectures
- **CDN (Content Delivery Network)** — a globally distributed network of 
  reverse-proxy/cache nodes that serve cached content near users and absorb 
  traffic spikes

A single piece of software (nginx, Envoy, HAProxy) can simultaneously act 
as a reverse proxy, load balancer, and caching layer — these are overlapping 
functions, not separate machines.

---

## Modern Usage of Proxy Servers

Proxy servers have evolved far beyond simple traffic routing. Here is how 
they show up in modern infrastructure:

**Security and Zero Trust**
Proxies are central to Zero Trust architecture — every request, even from 
inside the network, is intercepted and validated by a proxy before reaching 
the destination. Web Application Firewalls (WAFs) are reverse proxies that 
inspect HTTP traffic for attacks.

**Service Mesh**
In microservices architectures, a sidecar proxy (like Envoy in Istio) is 
deployed alongside every service instance. All inter-service traffic passes 
through these proxies, giving you observability, traffic control, and mutual 
TLS without changing application code.

**AI and LLM Traffic Management**
Increasingly, proxies are being used to manage traffic to LLM APIs — 
routing requests to different model providers, caching responses, enforcing 
rate limits, and logging prompts for compliance. Tools like LiteLLM and 
Portkey act as forward proxies for AI APIs.

**Privacy and Anonymity at Scale**
Tor's onion proxy routes traffic through at least three relays with layered 
encryption — the guard relay is the only one that knows the client's IP, 
and the exit relay is the only one that knows the target. Very high anonymity, 
at the cost of higher latency.

**Data Collection and Scraping**
Residential and rotating proxies are widely used for web scraping, price 
monitoring, and market research — using real ISP-assigned IPs to avoid 
detection, rotating them per request to avoid rate limiting.

**Spatial Locality Optimization**
A proxy can collapse requests for data that is spatially close together in 
storage. If multiple servers request different parts of the same file, a 
smart proxy recognizes the spatial locality, collapses them into a single 
read, and distributes the results — significantly reducing latency and 
minimizing reads from the data origin.