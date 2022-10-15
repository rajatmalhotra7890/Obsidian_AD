- LSA and LSASS stands for `Local Security Authority` and `Local Security Authority Subsystem Service`

## What is LSA?
- Local Security Authority is a protected system process that that authenticates and logs users to the local computer.
- Domain credentials are used by the OS and authenticated by the Local Security Authority.
- The LSA `can validate user information by checking the SAM database (Security Account Manager) located on the same computer.`
- The LSA is a user-mode process (`LSASS.exe`) used to store security information of a system known as `Local Security Policy`
	- The LSA maintains local security policy information in a set of objects


##### LSASS manages the local system policy, user authentication and auditing while handling sensitive security data such as password hashes and Kerberos keys.
- The secret part of domain credentials, the password is managed by the OS.


LSASS stores credentials in multiple forms like:
1. `Reversibly encrypted plaintext`
2. `Kerberos tickets (TGT, service tickets)`
3. `NT hash`
4. `LAN Manager Hash`



