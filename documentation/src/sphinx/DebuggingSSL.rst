.. contents::
   :depth: 3
..

.. raw:: html

   <!--- Copyright (C) 2009-2015 Typesafe Inc. <http://www.typesafe.com> -->

.. _DebuggingSSL:

Debugging SSL Connections
=========================

In the event that an HTTPS connection does not go through, debugging
JSSE can be a hassle.

WS SSL provides configuration options that will turn on JSSE debug
options defined in the `Debugging
Utilities <https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/JSSERefGuide.html#Debug>`__
and `Troubleshooting
Security <https://docs.oracle.com/javase/8/docs/technotes/guides/security/troubleshooting-security.html>`__
pages.

To configure, set the ``ssl-config.debug`` property in
``application.conf``:

::

    ssl-config.debug = {
        # Turn on all debugging
        all = false
        # Turn on ssl debugging
        ssl = false
        # Turn certpath debugging on
        certpath = false
        # Turn ocsp debugging on
        ocsp = false
        # Enable per-record tracing
        record = false
        # hex dump of record plaintext, requires record to be true
        plaintext = false
        # print raw SSL/TLS packets, requires record to be true
        packet = false
        # Print each handshake message
        handshake = false
        # Print hex dump of each handshake message, requires handshake to be true
        data = false
        # Enable verbose handshake message printing, requires handshake to be true
        verbose = false
        # Print key generation data
        keygen = false
        # Print session activity
        session = false
        # Print default SSL initialization
        defaultctx = false
        # Print SSLContext tracing
        sslctx = false
        # Print session cache tracing
        sessioncache = false
        # Print key manager tracing
        keymanager = false
        # Print trust manager tracing
        trustmanager = false
        # Turn pluggability debugging on
        pluggability = false
    }

    NOTE: This feature changes the setting of the ``java.net.debug``
    system property which is global on the JVM. In addition, this
    feature `changes static properties at
    runtime <https://tersesystems.com/2014/03/02/monkeypatching-java-classes/>`__,
    and is only intended for use in development environments.

Verbose Debugging
-----------------

To see the behavior of WS, you can configuring the SLF4J logger for
debug output:

::

    logger.play.api.libs.ws.ssl=DEBUG

Dynamic Debugging
-----------------

If you are working with WSClient instances created dynamically, you can
use the ``SSLDebugConfig`` class to set up debugging using a builder
pattern:

::

    val debugConfig = SSLDebugConfig().withKeyManager().withHandshake(data = true, verbose = true)

Further reading
---------------

Oracle has a number of sections on debugging JSSE issues:

-  `Debugging SSL/TLS
   connections <https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/ReadDebug.html>`__
-  `JSSE Debug Logging With
   Timestamp <https://blogs.oracle.com/xuelei/entry/jsse_debug_logging_with_timestamp>`__
-  `How to Analyze Java SSL
   Errors <http://www.smartjava.org/content/how-analyze-java-ssl-errors>`__
