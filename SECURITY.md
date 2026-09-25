# Security Considerations for ArkDeploy Toolkit

## Overview

ArkDeploy Toolkit is designed for use in trusted internal networks and lab environments. Several design decisions prioritize ease of use over complex security infrastructure. **This toolkit is NOT designed for untrusted or internet-facing deployments.**

---

## Critical Security Warnings

### 1. Plaintext Credentials in config.json

**Risk:** Server credentials are stored in plaintext in `config.json`.

```json
{
  "Server": {
    "Address": "yourserver",
    "Share": "yourshare",
    "User": "yourusername",
    "Passwd": "yourpassword"
  }
}
```

**Impact:**
- Anyone with read access to `config.json` can see the password
- The config file is copied to the ISO / bootable media root (visible to anyone who boots from the media)
- Compromised credentials could allow unauthorized access to the network share

**Mitigations:**
1. **Use a dedicated service account** with minimal privileges:
   - Read/write access ONLY to the deployment share
   - No administrative rights
   - No access to sensitive systems
   - Rotate credentials regularly

2. **Restrict file system permissions:**
   ```powershell
   # Restrict config.json to Administrators only (run as admin)
   $acl = Get-Acl ".\config.json"
   $acl.SetAccessRuleProtection($true, $false)
   $adminRule = New-Object System.Security.AccessControl.FileSystemAccessRule("BUILTIN\Administrators","FullControl","Allow")
   $acl.SetAccessRule($adminRule)
   Set-Acl ".\config.json" $acl
   ```

3. **Secure the deployment share:**
   - Use NTFS permissions to restrict access
   - Only allow the service account and administrators
   - Do not use Everyone or Domain Users permissions

4. **Physical security for PE media:**
   - Store bootable USBs securely when not in use
   - Do not leave PE media unattended in public areas
   - Destroy old PE media properly (secure wipe/destruction)

5. **Network isolation:**
   - Use PE media only on trusted internal networks
   - Consider VLAN isolation for deployment networks
   - Monitor access to the deployment share

---

### 2. SMB Security Considerations

**Risk:** Network credentials are transmitted over SMB during PE runtime.

**Mitigations:**
1. **Use SMB3 with encryption:**
   - Ensure your file server supports SMB 3.0+
   - Enable SMB encryption on the share:
     ```powershell
     Set-SmbShare -Name "DeploymentShare" -EncryptData $true
     ```

2. **Disable SMBv1:**
   ```powershell
   # On Windows Server
   Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
   
   # On Windows Client
   Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol-Client
   ```

3. **Use dedicated deployment VLAN:**
   - Isolate deployment traffic from production network
   - Use firewall rules to restrict SMB access to deployment subnet only

---

### 3. Unattended Installation Files

**Risk:** `unattend.xml` files may contain sensitive data (product keys, passwords, domain join credentials).

**Mitigations:**
1. **Do not store domain admin credentials** in unattend.xml
2. **Use local admin passwords only** for initial setup
3. **Store unattend.xml files outside the repository** if they contain sensitive data
4. Add `*unattend*.xml` to `.gitignore` if using Git
5. Consider using separate unattend files for different security zones

---

### 4. Driver and Update Security

**Risk:** Malicious drivers or updates could compromise deployed systems.

**Mitigations:**
1. **Only use drivers from trusted sources:**
   - Download directly from hardware manufacturer websites
   - Verify digital signatures on driver packages

2. **Validate Windows updates:**
   - Download MSU files only from Microsoft Update Catalog
   - Verify file hashes against Microsoft documentation

3. **Scan with antivirus:**
   - Run antivirus scans on `Assets\Drivers\` and `Assets\WU\` before building
   - Keep antivirus definitions up to date

---

### 5. Physical Access Security

**Risk:** Anyone with physical access can boot from PE media and access systems.

**Impact:**
- PE media boots with SYSTEM-level privileges
- Can access/modify any local disk
- Can deploy OS images and reconfigure systems
- Can capture images containing sensitive data

**Mitigations:**
1. **BIOS/UEFI security:**
   - Set BIOS/UEFI password on target systems
   - Disable boot from USB/CD in BIOS (when not deploying)
   - Enable Secure Boot where possible

2. **Physical security:**
   - Lock server rooms and deployment areas
   - Log all PE media usage
   - Track who has access to PE media
   - Implement check-out/check-in procedures for USB drives

3. **BitLocker considerations:**
   - PE media can be used to reformat BitLocker-protected drives
   - Suspend BitLocker before deployment or remove protectors
   - Re-enable BitLocker after deployment

---

### 6. Supply Chain Security

**Risk:** Compromised build host could inject malware into PE images.

**Mitigations:**
1. **Secure the build workstation:**
   - Use a dedicated, hardened workstation for builds
   - Keep Windows and ADK up to date
   - Run antivirus/antimalware
   - Restrict administrative access

2. **Verify ADK installation:**
   - Download Windows ADK only from official Microsoft sources
   - Verify installer hashes before running

3. **Code review:**
   - Review all scripts before running (especially after updates)
   - Understand what each script does
   - Check for unexpected network connections or file operations

---

## Best Practices for Secure Deployment

### For Lab/Test Environments
- Use separate credentials from production
- Isolate test network from production network
- Use test VMs instead of physical hardware where possible

### For Production Environments
1. **Change default credentials immediately** after downloading
2. **Implement change management:**
   - Document who builds PE media
   - Document when PE media is created
   - Track PE media version numbers
   - Maintain audit logs of deployments

3. **Regular security reviews:**
   - Review service account permissions quarterly
   - Rotate credentials regularly
   - Review deployment share access logs
   - Update security documentation

### Incident Response
If credentials are compromised:
1. **Immediately disable the service account**
2. **Audit deployment share access logs** for unauthorized access
3. **Destroy all PE media** containing compromised credentials
4. **Create new service account** with different password
5. **Rebuild PE media** with new credentials
6. **Investigate how credentials were compromised**

---

## Compliance Considerations

### GDPR / Data Protection
- PE capture operations may capture user data
- Ensure captured images are stored securely
- Implement data retention policies for captured images
- Document data processing activities

### Industry Standards
- **PCI DSS:** Do not store cardholder data on deployment shares
- **HIPAA:** Follow PHI storage requirements if deploying healthcare systems
- **SOC 2:** Document security controls for deployment infrastructure

---

## Reporting Security Issues

If you discover a security vulnerability in ArkDeploy Toolkit:

1. **Do not open a public GitHub issue**
2. Contact the maintainer privately at info@arkdeploy.com
3. Provide detailed steps to reproduce
4. Allow reasonable time for a fix before public disclosure

---

## Disclaimer

ArkDeploy Toolkit is provided "as-is" without warranty. Users are responsible for:
- Securing their deployment environment
- Protecting credentials and sensitive data
- Complying with organizational security policies
- Following applicable laws and regulations

**By using this toolkit, you acknowledge that you understand these security considerations and accept the risks involved.**
