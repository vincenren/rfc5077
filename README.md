Various tools for testing RFC 5077
==================================

[RFC 5077](http://tools.ietf.org/html/rfc5077) is a session resumption
mechanism for TLS without server-side state. You'll find here various
tools related to testing availability of RFC 5077.

This mechanism is an extension for TLS. If a client or a server does
not support TLS, it does not support RFC 5077.

Clients
-------

The following clients are implemented:

 - `openssl-client`
 - `gnutls-client`
 - `nss-client`

They all take an host and a port as argument. You need to use `-r`
flag to really test reconnection. You can also add `-T` to disable
ticket supports (RFC 5077) and `-S` to disable session ID
support. However, disabling session ID may be difficult, therefore, it
may not really have the expected effect.

Only OpenSSL client is complete enough. GNU TLS does not allow easy
display of session contents and NSS does not allow to check if a
session was resumed.

Additionally, `rfc5077-client` proposes some more advanced tests
against a server or a pool of servers. It will try to reuse sessions
with and without tickets and will query several time each IP of a pool
of servers. Use this if you want to check support of SSL session
resume of a server or a pool of servers.

It is possible that those clients may fail if you don't have a working
IPv6 connectivity. Get an IPv6 connectivity. ;-)

Servers
-------

`rfc5077-server` allows you to test support of RFC 5077 in the client
of your choice. It will returns an HTML page containing some
Javascript code to test browsers. You need to specify 4 ports. They
will respectively behave as follow:

 1. No session cache, no ticket support
 2. Session cache, no ticket support
 3. Session cache, ticket support
 4. No session cache, ticket support

This server can only serve on request simultanously. It is not meant
to be standard compliant. Don't put it on the Internet. Moreover,
it seems to choke on some clients, therefore it is buggy. Not the best
example to write your own server.