Summarized from https://security.stackexchange.com/questions/175749/what-are-the-functional-similarities-and-difference-between-tpm-and-sgx-in-trust

# Trusted Platform Modules
* **Goal**: verify boot process firmware
* TPM enables secure booting. Small secured layers bootstraps (verifies) the next stage in the chain of trust.
* The initial base is much smaller and is stored in the TPM. It stores firmware hashes for the first boot stage which thereby bootstraps trust for the remainder of the system.
* TPM can be verified by sysadmin and is resistant to tampering. It will only unseal data if firmware matches a stored hash.
* Remote attestation means that another client can pass a challenge to the TPM to verify that said machine is running signed and secure software.

# Secure Guard Extensions
* **Goal**: protect sensitive information from host machine
* Encrypts processes running in secure enclave to protect them. Processes verify that the enclave is secure and then the enclave can ensure processes are genuine. 
* SGX secures the enclave from all parties once it is set up. Only thing a process can do is kill a running process.
  * _Confidentiality_: data private to enclave
  * _Integrity_: outputs are correct in enclave
* Remote attestation means that a process can verify program loaded correctly in enclave
  * secured using intel cryptographic root of trust
