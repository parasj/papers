# Kerberos: An authentication service for open network systems

**Key idea**: Kerberos uses tickets to autheticate clients with any other clients. Both Kerberos and the client store the user's private key. Kerberos sends an encrypted ticket and session key to the client. The client decrypts the ticket using their private key and recrypts the ticket with the session key.

* How to authenticate clients on a network without passing around plaintext passwords?
* Kerberos uses ticket granting to authenticate users.
* How to secure networks?
    * On a single machine, the OS protects users from each other
    * In a networked environment where operator controls all computers, no protection may be needed.
    * In a networked environment without a dictator operator, there are a few options:
        * (1) clients can authenticate on opening a resource (like exokernel) but not after
        * (2) clients can authenticate every request
* Requirements
    * Secure
    * Reliable
    * Transparent
    * Scalable
