# Maximum Lifetime for Service Ticket

## Description

The "Maximum lifetime for service ticket" policy setting can greatly improve your organization's security. It configures the maximum duration (lifetime) that a granted session ticket can be used to access a service. If an expired session ticket is used from the client, the server returns an error, and the client must request a new session ticket from the Kerberos Distribution Center (KDC).

If this policy setting is configured for an extensive amount of time, users might be able to access resources outside their normal operating hours. Also, disabled accounts can still have access to services by using valid service tickets if they were issued before before the account became disabled.

## Priority Rating: High

## Related Attacks

1. Pass-the-Ticket Attacks: These attacks involve an attacker obtaining a Kerberos ticket-granting ticket (TGT) from a compromised user or service account. The attacker can then use this TGT to request service tickets and gain unauthorized access to resources within the organization. This technique is used for lateral movement by the adversary. Some example tools that can be used to perform this attack are Mimikatz, Crackmapexec, and Impacket.
2. Golden Ticket Attacks: In these attacks, an attacker gains access to the domain controller and creates a forged Kerberos ticket-granting ticket (TGT) with the accounts's NTLM hash. This forged ticket allows the attacker to impersonate any user in the domain and gain access to other domain wide resources. This technique requires the NTLM hash of the KRBTGT account This technique is used for persistence by the adversary. Some example tools that can be used to perform this attack are Mimikatz, Rubeus, and Impacket.

## Recommendation

Recommends setting the "Maximum lifetime for service ticket" to 600 minutes. This action will ensure that service tickets have a limited lifetime, enhancing the security of your organization. It should be noted that setting this policy will not interrupt existing sessions. The policy will only take effect when a new session ticket is requested.

### Domain Group Policy Configuration

1. Open Group Policy, this can be achieved by typing `gpmc.msc` in the Run dialog box.
2. Go to the domain/Organizational Unit (OU) where you want to apply the policy.
3. Right-click on the domain/OU, then select Create a GPO in this domain, and Link it.
4. Name the new Group Policy Object (GPO), then click OK.
5. Right-click on the new GPO and select Edit.
6. In Group Policy Management, go to the following path:
Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Policies -> Kerberos Policy
7. Find and double-click on "Maximum lifetime for service ticket".
8. In the properties dialog box, set the value to 600 minutes.
9. Click OK to close the properties dialog box.
10. Close Group Policy Management.

The changes will take effect after the Group Policy is updated. You can force an update by running `gpupdate /force` in the command prompt on the target machines.

## References

<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/maximum-lifetime-for-service-ticket>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/administer-security-policy-settings>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/kerberos-policy>
<https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-kile/b4af186e-b2ff-43f9-b18e-eedb366abf13>
<https://adsecurity.org/?p=556>
<https://blog.gentilkiwi.com/securite/mimikatz/pass-the-ticket-kerberos>
<https://github.com/GhostPack/Rubeus>
<https://adsecurity.org/?p=1640>
<https://adsecurity.org/?p=2011>
