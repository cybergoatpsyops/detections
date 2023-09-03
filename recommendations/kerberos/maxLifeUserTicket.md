# Maximum Lifetime for User Tickets

## Description

The "Maximum lifetime for user tickets" policy setting can greatly improve of your organization's security. It configures the maximum amount of time (lifetime) that a user’s ticket-granting ticket (tgt) can be used. When a user’s tgt expires, a new one must be requested or the existing one must be renewed.

If this policy setting is configured for an extensive amount of time, users might be able to access resources outside of their normal operating hours. Also, disabled accounts might still have access to access network services by using valid service tickets that were issued before their account was disabled. If this setting is set to 0, tgt never expires.

## Priority Rating: Medium

## Related Attacks

1. Pass-the-Ticket Attacks: These attacks involve an attacker obtaining a Kerberos ticket-granting ticket (TGT) from a compromised user or service account. The attacker can then use this TGT to request service tickets and gain unauthorized access to resources within the organization. This technique is used for lateral movement by the adversary. Some example tools that can be used to perform this attack are Mimikatz, Crackmapexec, and Impacket.
2. Golden Ticket Attacks: In these attacks, an attacker gains access to the domain controller and creates a forged Kerberos ticket-granting ticket (TGT) with the accounts's NTLM hash. This forged ticket allows the attacker to impersonate any user in the domain and gain access to other domain wide resources. This technique requires the NTLM hash of the KRBTGT account This technique is used for persistence by the adversary. Some example tools that can be used to perform this attack are Mimikatz, Rubeus, and Impacket.

## Recommendation

Recommends setting the "Maximum lifetime for user ticket" setting with a value between 4 and 10 hours. This action will ensure that user tickets are not used beyond the user's logon hours, enhancing the security of your organization.

### Domain Group Policy Configuration

1. Open the Group Policy Management Console by typing gpmc.msc in the Run dialog box.
2. Go to the domain/Organizational Unit (OU) where you want to apply the policy.
3. Right-click on the domain/OU, then select Create a GPO in this domain, and Link it.
4. Name the new Group Policy Object (GPO), then click OK.
5. Right-click on the new GPO and select Edit.
6. In Group Policy Management, go to the following path:the value for this policy setting is too high
Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Policies -> Kerberos Policy
7. Find and double-click on "Maximum lifetime for user ticket".
8. In the properties dialog box, set the desired value between 4 and 10 hours, then click OK.
9. Close Group Policy Management.

The changes will take effect after the Group Policy is updated. You can force an update by running gpupdate /force in the command prompt on the target machines.

## References

<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/maximum-lifetime-for-user-ticket>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/user-rights-assignment>
<https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-kile/b4af186e-b2ff-43f9-b18e-eedb366abf13>
<https://adsecurity.org/?p=556>
<https://blog.gentilkiwi.com/securite/mimikatz/pass-the-ticket-kerberos>
<https://github.com/GhostPack/Rubeus>
<https://adsecurity.org/?p=1640>
<https://adsecurity.org/?p=2011>
