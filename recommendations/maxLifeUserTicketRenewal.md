# Maximum Lifetime for User Ticket Renewal

## Description

The "Maximum lifetime for user ticket renewal" policy setting is a crucial aspect of your organization's security. It determines the maximum period (in days) during which a user’s ticket-granting ticket can be renewed.

If this policy setting is configured for an extensive amount of time, users might be able to renew old user tickets, potentially leading to unauthorized access to resources.

## Priority Rating: High

## Related Attacks

1. Pass-the-Ticket Attacks: These attacks involve an attacker obtaining a Kerberos ticket-granting ticket (TGT) from a compromised user or service account. The attacker can then use this TGT to request service tickets and gain unauthorized access to resources within the organization. This technique is used for lateral movement by the adversary. Some example tools that can be used to perform this attack are Mimikatz, Crackmapexec, and Impacket.
2. Golden Ticket Attacks: In these attacks, an attacker gains access to the domain controller and creates a forged Kerberos ticket-granting ticket (TGT) with the accounts's NTLM hash. This forged ticket allows the attacker to impersonate any user in the domain and gain access to other domain wide resources. This technique requires the NTLM hash of the KRBTGT account This technique is used for persistence by the adversary. Some example tools that can be used to perform this attack are Mimikatz, Rubeus, and Impacket.
3. Silver Ticket Attacks: These attacks involve an attacker creating a forged service ticket for a specific service on the network. By using this forged ticket, the attacker can authenticate to the service and gain unauthorized access to its resources. This technique requires the NTLM hash of a specific service account This technique is used for persistence by the adversary. Some example tools that can be used to perform this attack are AADInternals, Empire, and Rubeus.
4. Overpass-the-Hash Attacks: In these attacks, an attacker obtains the NTLM hash of a user's password and uses it to authenticate as the user without knowing the actual password. This attack can be performed using tools like Mimikatz and can be used to request TGTs, which could bypass the maximum lifetime for user ticket renewal. This technique is used for lateral movement by the adversary.Some examples of tools that can be used to perform this attack are Mimikatz, Rubeus, and Impacket.

## Recommendation

Recommends setting the "Maximum lifetime for user ticket renewal" to 7 days. This action will ensure that user tickets have a limited lifetime, enhancing the security of your organization.

### Domain Group Policy Configuration

1. Open Group Policy, this can be achieved by typing `gpmc.msc` in the Run dialog box.
2. Go to the domain/Organizational Unit (OU) where you want to apply the policy.
3. Right-click on the domain/OU, then select Create a GPO in this domain, and Link it.
4. Name the new Group Policy Object (GPO), then click OK.
5. Right-click on the new GPO and select Edit.
6. In Group Policy Management, go to the following path:
Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Policies -> Kerberos Policy
7. Find and double-click on "Maximum lifetime for user ticket renewal".
8. In the properties dialog box, set the value to 7 days.
9. Click OK to close the properties dialog box.
10. Close Group Policy Management.

The changes will take effect after the Group Policy is updated. You can force an update by running `gpupdate /force` in the command prompt on the target machines.

## References

<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/maximum-lifetime-for-user-ticket-renewal>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/administer-security-policy-settings>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/kerberos-policy>
<https://adsecurity.org/?p=556>
<https://blog.gentilkiwi.com/securite/mimikatz/pass-the-ticket-kerberos>
<https://github.com/GhostPack/Rubeus>
<https://adsecurity.org/?p=1640>
<https://adsecurity.org/?p=2011>
<https://www.ultimatewindowssecurity.com/wiki/page.aspx?spid=MaxLifeUsrTxRnwl>
