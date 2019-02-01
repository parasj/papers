# Making Information Flow Explicit in HiStar

**Key Idea**: Secure OS by restricting information flow. User data is marked as "tainted" and thus is restricted from leaving the computer. Thus data cannot leak from the computer. Only a small core of code need be verified. 

* Idea: simplicity leads to security
* Explicit access checks on information flows can prevent data leaks
* Chroots protect against similar issues but paper claims that chroots can break compatibility. More than HiStar does though?
* Model data as tainted if it is private user data.
  * monitoring data tainting can prevent data leaking
* Related work is SELinux, EROS, Abestos. Ideas of controlling information flow aren't new.
