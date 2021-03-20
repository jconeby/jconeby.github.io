

### Active Directory Domain Controllers 

<br>

####Domain Controller (DC)

- The component hosting all the Active Directory functionality and protocols.  It stores directory data and manages user and domain interactions, including user logon processes, authentication, and directory searches.  If privileged access to a DC is obtained by a malicious user, they can modify or destroy the entire Active Directory database.

<br>

####Primary Roles

1. Stores and maintains a copy of the Directory Services database
2. To replicate changes to the database to other domain controllers
3. Used to provide redundancy if one of the domain controllers fails
4. To deliver a means for managing and administering the objects in the domain
5. Performs identification and authentication, and manages the application of policy within the domain


<br>

####Common Domain Controller Security Mistakes

- **Too Many Domain Admins**: Since Domain Admins have full admin rights to all workstations, servers, DCs, Active Directory, and Group Policy by default, the members of this group should be kept to a minimum.
  
- **Over-Permissioned Service Accounts**: Often, service accounts will be given Domain Admin rights because it makes the product easier to deploy.  However, it is often forgotten that the service running has the credential stored in LSASS which could be extracted by an attacker.
  
- **Service Account Weak Passwords**: It is easy to request TGS service tickets encrypted with a Service Account's password.  Once the ticket is received, it can be brute forced offline.  If the password is weak, then it is likely the password will be determined.
  
- **Insecurely Storing Credentials**: Active Directory Admins have been known to sometimes store credentials inside group policy objects.  Attackers can easily query GPOs and will likely find the credentials.

<br>

####Securing Domain Controllers

- An organization should recognize domain controllers as critical infrastructure components and should be treated as such when securing.

- Limit the applications and utilities that are installed on the domain controller.  By having unneeded applications or services, it increases the attack surface of the DC.

- Ensure that users with high levels of privilege are not browsing the internet on the domain controller.

- Use Group Policy Objects (GPOs) to configure and enforce security settings.

- The DC should be configured with Trusted Platform Module (TPM) chips and all volumes in the DC servers should be protected with full disk encryption.

- Virtual DCs should be run on seperate physical hosts than other virtual machines in the environment.

- Configure the perimeter firewall to block outbound connections from the DC to the Internet






