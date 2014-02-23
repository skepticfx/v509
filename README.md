V.509
=====

Validate your X.509 certificate implementations.

**This is just an idea and nothing works now. Stay tuned!**

### The Idea 

The idea is to check TLS clients, especially non-browser clients to see how well they validate the X.509 certificates. This is  the certificate which the server provides to the client, to prove itself. 

X.509 is the standard used by these certificates. There are some interesting test cases that can conducted to know how well these certificates are validated. The following RFC proposal does a very good job of listing down all the important checks to be made. 
[RFC 6125 -   Representation and Verification of Domain-Based Application Service Identity within Internet Public Key Infrastructure Using X.509 (PKIX) Certificates in the Context of Transport Layer Security](https://tools.ietf.org/html/rfc6125)

### Architecture

Since the TLS clients are going to be tested for their implementations, we are talking about an heterogeneous environment. The best way to handle this is to expose a form of REST APIs to tell the validation server about the states happening in the client. This includes *START, STOP* etc. The tester has to write custom scripts on the client machine to facilitate, complete testing. 

Also, the validator knows whenever it presents a certain certificate, that whether it is a good or bad one. That way depending upon the TLS alerts / errors, the validator can know what is going on. 

The validator is a NodeJS server which listens on a given domain name. Say, **v509.com** . This domain name has to be configured on the client side using /etc/hosts or by having a DNS configuration which sends all traffic to the validator. The Validator requires the host name to start itself( Eg. v509.com).
Also, the client has to be configured with a CA which the validator gives. This shall be used only during the testing and can be removed later.

The validator should generate certificates on the fly depending upon the test cases and provide it to the client to do the test.


### TODO

* Generate custom certificates for the given host name and other X.509 artifacts, from the cert-test-suite.
* Make a modular cert-test-suite which specifies the Test Name, X.509 fields, Good / Bad and other constraints.
* A REST API which says the validator to START and STOP the scans.
* Config scripts to do the dirty job on the client side.

### Existing work

* TLSPretense - Am not so impressed with it and needs a lot more than this.

### Critics and comments

I would love to know your thoughts on what will work and what won't. You should create a new issue with your critics / comments.
