## Performance vs security tradeoff
Meltdown, Spectre show that there is a performance-security tradeoff that is made in systems. In order to provide highly secure systems, there is increased performance overhead. Microkernel vs monolithic kernels show that the increased security from microkernels leads to a performance hit.

## Denning's Data Security guidelines
* Access controls
  * Limit access to objects to users.
  * Requirements:
    * User identification
      * Passwords, something you know. But have issues.
      * OTP, something you have
      * Biometrics, something you are
    * No snooping on the network or backups (encryption can address this)
    * Controlled access control lists
* Flow controls
  * Prevent information from being transmitted from one part of the system to another. Idea behind HiStar.
  * Data has a particular level of security and cannot be lowered
  * Data can become overclassified as programs may interact with data across classes
  * Covert channels are hard to stop
  * Have to be careful to prevent people from copying data
* Inference controls
  * Ability for users to determine specific information in a database
  * E.g. leaking metadata
  * Mitigations:
    * Restricting queries
    * Distorting data responses
    * Random sampling
* Cryptographic controls
  * Symmetric encryption vs asymmetric encryption
