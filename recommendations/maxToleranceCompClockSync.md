# Maximum Tolerance for Computer Clock Synchronization

## Description

The "Maximum tolerance for computer clock synchronization" policy setting is important to your organization's security. It determines the maximum time sync difference in Kerberos between the client and the domain controller that is required in Kerberos authentication.

If this policy setting is configured for too much time, it could lead to replay attacks, where an authentication credential is resubmitted by a malicious user or program to gain access to a protected resource.

## Priority Rating: High

## Related Attacks

1. Replay Attacks: These attacks involve the adversary acting as a Man-in-the-Middle (MitM) resubmitting an authentication credential to gain access to a protected resource. The Kerberos protocol uses time stamps as part of its definition to prevent such attacks. If the client computer clock and the domain controller clock are not closely synchronized, it could lead to successful replay attacks. This attack is considered a credential access technique. Some example tools that can be used to perform this attack are Mimikatz and Crackmapexec.

2. Kerberoasting: This attack involves exploiting the Kerberos Service Principal Names (SPNs) to crack the passwords of service accounts. If the clocks are not synchronized, such attacks are possible. This is consider a credential access technique. Some tools known to be used for this attack are Empire, Rubeus, and Impacket.

3. Golden Ticket Attacks: In these attacks, an attacker gains access to the domain controller and creates a forged Kerberos ticket-granting ticket (TGT) with the accounts's NTLM hash. This forged ticket allows the attacker to impersonate any user in the domain and gain access to other domain wide resources. This technique requires the NTLM hash of the KRBTGT account. This technique is used for persistence by the adversary. Some example tools that can be used to perform this attack are Mimikatz, Rubeus, and Impacket.

## Recommendation

Recommends "Maximum tolerance for computer clock synchronization" to 5 minutes. This will ensure that the time difference by Kerberos is limited, enhancing the security of your organization.

### Domain Group Policy Configuration

1. Open Group Policy, this can be achieved by typing `gpmc.msc` in the Run dialog box.
2. Go to the domain/Organizational Unit (OU) where you want to apply the policy.
3. Right-click on the domain/OU, then select Create a GPO in this domain, and Link it.
4. Name the new Group Policy Object (GPO), then click OK.
5. Right-click on the new GPO and select Edit.
6. In Group Policy Management, go to the following path:
Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Policies -> Kerberos Policy
7. Find and double-click on "Maximum tolerance for computer clock synchronization".
8. In the properties dialog box, set the value to 5 minutes.
9. Click OK to close the properties dialog box.
10. Close Group Policy Management.

The changes will take effect after the Group Policy is updated. You can force an update by running `gpupdate /force` in the command prompt on the target machines.

## References

<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/maximum-tolerance-for-computer-clock-synchronization>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/administer-security-policy-settings>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/kerberos-policy>
<https://www.sentinelone.com/cybersecurity-101/what-is-kerberoasting-attack/>
<https://medium.com/@ivecodoe/windows-event-id-4649-a-replay-attack-was-detected-ab02968d91ee>
<https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4649>
<https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Active%20Directory%20Attack.md#replay-kerberos-tickets>
