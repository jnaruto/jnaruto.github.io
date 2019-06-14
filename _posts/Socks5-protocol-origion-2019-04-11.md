---
layout:     post
title:      VPS 測速
subtitle:   6-14
date:       2019-06-14
author:     naruto
header-img: img/post-bg-os-metro.jpg
catalog: true
tags:
    - Network
---

# Status of this Memo
<p class="section-indent">
This document specifies an Internet standards track protocol for the
Internet community, and requests discussion and suggestions for
improvements.  Please refer to the current edition of the "Internet
Official Protocol Standards" (STD 1) for the standardization state
and status of this protocol.  Distribution of this memo is unlimited.
</p>

## Acknowledgments
<p class="section-indent">
This memo describes a protocol that is an evolution of the previous
   version of the protocol, version 4 [1]. This new protocol stems from
   active discussions and prototype implementations.  The key
   contributors are: Marcus Leech: Bell-Northern Research, David Koblas:
   Independent Consultant, Ying-Da Lee: NEC Systems Laboratory, LaMont
   Jones: Hewlett-Packard Company, Ron Kuris: Unify Corporation, Matt
   Ganis: International Business Machines.
</p>

## Introduction
<p class="section-indent">
	The use of network firewalls, systems that effectively isolate an
   organizations internal network structure from an exterior network,
   such as the INTERNET is becoming increasingly popular.  These
   firewall systems typically act as application-layer gateways between
   networks, usually offering controlled TELNET, FTP, and SMTP access.
   With the emergence of more sophisticated application layer protocols
   designed to facilitate global information discovery, there exists a
   need to provide a general framework for these protocols to
   transparently and securely traverse a firewall.
</p>
----

<p class="section-indent">
	There exists, also, a need for strong authentication of such
   traversal in as fine-grained a manner as is practical. This
   requirement stems from the realization that client-server
   relationships emerge between the networks of various organizations,
   and that such relationships need to be controlled and often strongly
   authenticated.<br>

   The protocol described here is designed to provide a framework for
   client-server applications in both the TCP and UDP domains to
   conveniently and securely use the services of a network firewall.
   The protocol is conceptually a "shim-layer" between the application
   layer and the transport layer, and as such does not provide network-
   layer gateway services, such as forwarding of ICMP messages.
</p>
## Existing practice
<p class="section-indent">
 There currently exists a protocol, SOCKS Version 4, that provides for
   unsecured firewall traversal for TCP-based client-server
   applications, including TELNET, FTP and the popular information-
   discovery protocols such as HTTP, WAIS and GOPHER.<br>
   This new protocol extends the SOCKS Version 4 model to include UDP,
   and extends the framework to include provisions for generalized
   strong authentication schemes, and extends the addressing scheme to
   encompass domain-name and V6 IP addresses. <br>
   The implementation of the SOCKS protocol typically involves the
   recompilation or relinking of TCP-based client applications to use
   the appropriate encapsulation routines in the SOCKS library.<br>
</p>
 
<p class="section-indent">
	Unless otherwise noted, the decimal numbers appearing in packet-
   format diagrams represent the length of the corresponding field, in
   octets.  Where a given octet must take on a specific value, the
   syntax X'hh' is used to denote the value of the single octet in that
   field. When the word 'Variable' is used, it indicates that the
   corresponding field has a variable length defined either by an
   associated (one or two octet) length field, or by a data type field.
</p>
## Procedure for TCP-based clients
<p class="section-indent">
	When a TCP-based client wishes to establish a connection to an object
   that is reachable only via a firewall (such determination is left up
   to the implementation), it must open a TCP connection to the
   appropriate SOCKS port on the SOCKS server system.  The SOCKS service
   is conventionally located on TCP port 1080.  If the connection
   request succeeds, the client enters a negotiation for the authentication method to be used, authenticates with the chosen
   method, then sends a relay request.  The SOCKS server evaluates the
   request, and either establishes the appropriate connection or denies
   it. <br>

   Unless otherwise noted, the decimal numbers appearing in packet-
   format diagrams represent the length of the corresponding field, in
   octets.  Where a given octet must take on a specific value, the
   syntax X'hh' is used to denote the value of the single octet in that
   field. When the word 'Variable' is used, it indicates that the
   corresponding field has a variable length defined either by an
   associated (one or two octet) length field, or by a data type field.

   The client connects to the server, and sends a version
   identifier/method selection message:
</p>
----
<html>
 +----+----------+----------+
 |VER | NMETHODS | METHODS  |
 +----+----------+----------+
 | 1  |    1     | 1 to 255 |
 +----+----------+----------+
</html>
<p class="section-indent">
 The VER field is set to X'05' for this version of the protocol.  The
   NMETHODS field contains the number of method identifier octets that
   appear in the METHODS field.
<br>
   The server selects from one of the methods given in METHODS, and
   sends a METHOD selection message:
</p>
<html>
                         +----+--------+
                         |VER | METHOD |
                         +----+--------+
                         | 1  |   1    |
                         +----+--------+
</html>
<p class="section-indent">

</p>
<p class="section-indent">

</p>

<p class="section-indent">

</p>


<p class="section-indent">

</p>
