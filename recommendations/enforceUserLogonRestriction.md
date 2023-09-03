# Enforce User Logon Restrictions

## Description

The "Enforce user logon restrictions" policy setting is a critical component of your network's security. It determines whether the Kerberos V5 Key Distribution Center (KDC) validates every request for a session ticket against the user rights policy of the user account. Although this validation is optional and can potentially slow network access to services, it is a crucial step in preventing unauthorized access. If this policy setting is disabled, users might be granted session tickets for services that they don't have the right to use.

## Priority Rating: Medium

## Related Attacks

1. Pass-the-Ticket Attacks: These attacks involve an attacker obtaining a Kerberos ticket-granting ticket (TGT) from a compromised user or service account. The attacker can then use this TGT to request service tickets and gain unauthorized access to resources within the organization. This technique is used for lateral movement by the adversary. Some example tools that can be used to perform this attack are Mimikatz, Crackmapexec, and Impacket.
2. Golden Ticket Attacks: In these attacks, an attacker gains access to the domain controller and creates a forged Kerberos ticket-granting ticket (TGT) with the accounts's NTLM hash. This forged ticket allows the attacker to impersonate any user in the domain and gain access to other domain wide resources. This technique requires the NTLM hash of the KRBTGT account This technique is used for persistence by the adversary. Some example tools that can be used to perform this attack are Mimikatz, Rubeus, and Impacket.
3. Silver Ticket Attacks: These attacks involve an attacker creating a forged service ticket for a specific service on the network. By using this forged ticket, the attacker can authenticate to the service and gain unauthorized access to its resources. This technique requires the NTLM hash of a specific service account This technique is used for persistence by the adversary. Some example tools that can be used to perform this attack are AADInternals, Empire, and Rubeus.

## Recommendation

Recommend enabling the "Enforce user logon restrictions" setting. This action will ensure that every request for a session ticket is validated against the user rights policy of the user account, thereby enhancing the security of your organization.

### Domain Group Policy Configuration

1. Open Group Policy by typing `gpmc.msc` in the Run dialog box.
2. Go to the domain/Organizational Unit (OU) where you want to apply the policy.
3. Right-click on the domain/OU, then select Create a GPO in this domain, and Link it.
4. Name the new Group Policy Object (GPO), then click OK.
5. Right-click on the new GPO and select Edit.
6. In Group Policy Management, go to the following path:
Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Local Policies -> User Rights Assignment
7. Find and double-click on "Access this computer from the network".
8. In the properties dialog box, click on Add User or Group button.
9. In the Select Users, Computers, Service Accounts, or Groups dialog box, enter the name of the user or group that you want to add, and then click OK.
10. Click OK again to close the properties dialog box.
11. Close Group Policy Management.

The changes will take effect after the Group Policy is updated. You can force an update by running `gpupdate /force` in the command prompt on the target machines.

## References

<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/enforce-user-logon-restrictions>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/user-rights-assignment>
<https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-kile/b4af186e-b2ff-43f9-b18e-eedb366abf13>
<https://adsecurity.org/?p=556>
<https://blog.gentilkiwi.com/securite/mimikatz/pass-the-ticket-kerberos>
<https://github.com/GhostPack/Rubeus>
<https://adsecurity.org/?p=1640>
<https://adsecurity.org/?p=2011>
