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

## Password Policy Configuration

The existing domain password policy was reviewed before making changes.

The original configuration included:

- **Password history:** 24 passwords remembered
- **Maximum password age:** 42 days
- **Minimum password age:** 1 day
- **Minimum password length:** 7 characters
- **Password complexity:** Enabled
- **Reversible encryption:** Disabled

![Password Policy Before Configuration](screenshots/account-security/02-password-policy-before-configuration.png)

To strengthen the password baseline, the minimum password length was increased from **7 characters to 12 characters**.

The existing password history, complexity, password age, and reversible encryption settings were retained.

The resulting policy requires domain users to create passwords of at least 12 characters while continuing to enforce Windows password complexity requirements.

![Password Policy Configured](screenshots/account-security/03-password-policy-configured.png)

## Account Lockout Policy

The existing Account Lockout Policy was also reviewed.

Initially, the **account lockout threshold was set to 0 invalid logon attempts**, meaning domain accounts would not automatically lock after repeated failed authentication attempts.

![Account Lockout Policy Before Configuration](screenshots/account-security/04-account-lockout-policy-before-configuration.png)

To provide protection against repeated password-guessing attempts, the following account lockout settings were configured:

- **Account lockout threshold:** 3 invalid logon attempts
- **Account lockout duration:** 30 minutes
- **Reset account lockout counter after:** 30 minutes

This means that three consecutive failed authentication attempts will lock the domain account for 30 minutes unless an administrator manually unlocks it earlier.

![Account Lockout Policy Configured](screenshots/account-security/05-account-lockout-policy-configured.png)

## Applying and Verifying the Domain Account Policy

After configuring the domain account policies, Group Policy was refreshed on `CLIENT01` using an elevated Command Prompt:

`gpupdate /force`

Both the Computer Policy and User Policy updates completed successfully.

![CLIENT01 Account Policy Group Policy Update](screenshots/account-security/06-client01-account-policy-gpupdate.png)

The effective domain account policy was then verified from `CLIENT01` using:

`net accounts /domain`

The command confirmed that the workstation was receiving the expected domain settings, including:

- **Minimum password length:** 12 characters
- **Password history:** 24 passwords
- **Lockout threshold:** 3 attempts
- **Lockout duration:** 30 minutes
- **Lockout observation window:** 30 minutes

This validated that the configured account security settings were active within the `cybershield.test` domain.

![Domain Account Policy Verified](screenshots/account-security/07-domain-account-policy-verified.png)

## First-Logon Password Change

The `bob.islam` domain account was configured with **User must change password at next logon**.

When Bob attempted to sign in to `CLIENT01` using the administrator-assigned initial password, Windows required the password to be changed before access to the workstation was granted.

![First Logon Password Change Required](screenshots/account-security/08a-first-logon-password-change-required.png)

Bob was then presented with the password change interface, allowing the initial password to be replaced with a private password that complied with the domain password policy.

This demonstrates a common account-provisioning practice where an administrator creates an account with an initial password but the user is required to choose their own password during first sign-in.

![First Logon Password Change Screen](screenshots/account-security/08b-first-logon-password-change-screen.png)

## Account Lockout Testing and Recovery

To validate the configured account lockout policy, three incorrect authentication attempts were deliberately made against the `bob.islam` domain account from `CLIENT01`.

After three failed attempts, the configured account lockout threshold was reached.

![Bob Three Failed Logon Attempts](screenshots/account-security/09-bob-three-failed-logon-attempts.png)

The account status was then investigated on `DC01` using Active Directory Users and Computers.

Bob's account properties confirmed:

**This account is currently locked out on this Active Directory Domain Controller.**

This demonstrates how an IT support technician can distinguish an account lockout from other authentication problems such as an incorrect password or disabled account.

![Bob Account Locked in Active Directory](screenshots/account-security/10-bob-account-locked-in-active-directory.png)

The account was manually unlocked by the administrator without resetting Bob's password.

Authentication was then tested again from `CLIENT01` using Bob's existing password. A Command Prompt was successfully launched under Bob's domain credentials and `whoami` returned:

`cybershield\bob.islam`

This confirmed that the account had been successfully unlocked and that a password reset was not required.

![Bob Account Unlock Verified](screenshots/account-security/11-bob-account-unlock-verified.png)

## Helpdesk Password Reset

A separate helpdesk scenario was performed to simulate a user who had forgotten their password.

Using Active Directory Users and Computers on `DC01`, the administrator selected **Reset Password** for the `bob.islam` account.

The option **User must change password at next logon** was enabled so that the administrator could provide a temporary password without determining the user's final private password.

Bob's account was already unlocked, so the separate **Unlock the user's account** option was not required.

![Helpdesk Password Reset Dialog](screenshots/account-security/12-helpdesk-password-reset-dialog.png)

After entering a temporary password that complied with the domain password policy, Active Directory confirmed that Bob's password had been successfully changed.

![Helpdesk Password Reset Success](screenshots/account-security/13-helpdesk-password-reset-success.png)

## Forced Password Change After Reset

Bob then attempted to sign in to `CLIENT01` using the temporary password.

Because **User must change password at next logon** had been selected during the administrative reset, Windows required Bob to create a new password before completing the sign-in process.

![Password Reset Change Required](screenshots/account-security/14-password-reset-change-required.png)

## Password History Enforcement

During the password change, an attempt was made to reuse a previously used password.

Windows rejected the password and displayed a message explaining that the password did not meet the domain's password requirements.

In this test, the reused password was prevented by the configured password-history policy, which remembers the previous **24 passwords**.

![Password History Policy Enforced](screenshots/account-security/15-password-history-policy-enforced.png)

A different password meeting the domain requirements was then entered successfully, and Windows confirmed that the password had been changed.

This validated the password-reset workflow as well as enforcement of the domain password policy during a user-initiated password change.

![User Password Change Success](screenshots/account-security/16-user-password-change-success.png)

## Disabling and Re-Enabling a Domain Account

Another common account-administration scenario was tested by temporarily disabling the `bob.islam` domain account.

Disabling an account prevents the user from authenticating while preserving the Active Directory account, group memberships, and associated configuration.

Using Active Directory Users and Computers on `DC01`, the administrator selected **Disable Account** for Bob.

![Disable Domain User Account](screenshots/account-security/17-disable-domain-user-account.png)

Active Directory confirmed that the `Bob Islam` account had been successfully disabled.

![Domain User Account Disabled](screenshots/account-security/18-domain-user-account-disabled.png)

## Verifying Access Is Denied

An authentication attempt was then made from `CLIENT01` using Bob's correct credentials.

Windows refused the sign-in and displayed:

**Your account has been disabled. Please see your system administrator.**

This demonstrated that disabling the Active Directory account immediately prevented the user from authenticating, independently of whether the supplied password was correct.

![Disabled Account Logon Denied](screenshots/account-security/19-disabled-account-logon-denied.png)

## Re-Enabling and Verifying the Account

After completing the disabled-account test, Bob's domain account was re-enabled through Active Directory Users and Computers.

Active Directory confirmed that the account had been successfully enabled.

![Domain User Account Enabled](screenshots/account-security/20-domain-user-account-enabled.png)

Bob was then able to authenticate to `CLIENT01` again using his existing credentials.

The `whoami` command returned:

`cybershield\bob.islam`

This confirmed that re-enabling the account restored authentication without requiring the account to be recreated or the password to be reset.

![Re-Enabled Account Logon Verified](screenshots/account-security/21-re-enabled-account-logon-verified.png)

## Validation and Learning Outcome

The Account and Password Security implementation was successfully configured and tested across the `cybershield.test` Active Directory environment.

Rather than only configuring Group Policy settings, each control was practically tested from both the administrator and end-user perspectives.

The completed lab demonstrated:

- Reviewing domain Account Policies through Group Policy
- Increasing the minimum domain password length from 7 to 12 characters
- Maintaining password complexity and password history requirements
- Configuring an account lockout threshold of 3 failed authentication attempts
- Configuring a 30-minute account lockout duration and observation window
- Applying updated domain policies to a domain-joined workstation
- Verifying effective account policy using `net accounts /domain`
- Enforcing password changes during a user's first domain logon
- Deliberately triggering and diagnosing an Active Directory account lockout
- Unlocking a domain account without unnecessarily resetting its password
- Performing an administrator-initiated password reset
- Requiring a user to replace a temporary password at next logon
- Demonstrating password-history enforcement when an old password was reused
- Disabling a domain account and verifying that authentication was denied
- Re-enabling the account and confirming that authentication was restored

## Helpdesk Skills Demonstrated

This section also provided practical experience with several common IT support scenarios.

A key learning outcome was understanding that authentication problems can have different causes and should be diagnosed before administrative changes are made.

For example:

- **Incorrect password** — authentication fails, but the account may still be active.
- **Locked account** — repeated failed authentication has triggered the domain lockout policy.
- **Disabled account** — authentication is intentionally prevented by an administrator.
- **Forgotten password** — an administrator may reset the password and require the user to change the temporary password at next logon.

These scenarios require different administrative responses. In particular, unlocking an account does not automatically require a password reset, and disabling an account does not delete the Active Directory user object.

The overall workflow demonstrated throughout this section was:

`Configure → Apply → Test → Diagnose → Administer → Verify`

This provided hands-on experience with centralized account security as well as realistic Active Directory helpdesk administration.
