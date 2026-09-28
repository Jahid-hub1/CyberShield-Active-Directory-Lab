# 07 - Account & Password Security

This section documents the implementation and practical testing of domain account security within the `cybershield.test` Active Directory environment.

The objective was not only to configure security policies, but also to simulate common IT helpdesk and user account administration scenarios using `DC01` and the domain-joined `CLIENT01` workstation.

The implementation demonstrates:

- Configuring domain password policy
- Increasing the minimum password length
- Configuring account lockout protection
- Verifying effective domain account policies from a workstation
- Enforcing password changes at first logon
- Testing account lockout after repeated failed authentication attempts
- Diagnosing and unlocking locked domain accounts
- Performing administrator password resets
- Enforcing password history requirements
- Disabling and re-enabling domain user accounts
- Verifying account access after administrative changes

## Domain Account Policy

Domain password and account lockout policies are centrally managed through Group Policy.

The account policies were reviewed within the `Default Domain Policy` under:

`Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies`

This location contains the domain's **Password Policy**, **Account Lockout Policy**, and **Kerberos Policy** settings.

![Default Domain Account Policies](screenshots/account-security/01-default-domain-account-policies.png)

