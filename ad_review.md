

# Active Directory Review 

<br>

Many organizations use Active Directory to manage their network and resources.  Due to Active Directory being used by so many entities, it has become a target for attack. In addition, threat actors continue to discover new TTPs to strike Active Directory environments.

<br>

Security in Active Directory is paramount because if an attacker gains highly privileged access to a domain or domain controller, that access can be leveraged to access, control, or even destroy an entire Active Directory forest.

<br>

####Active Directory Benefits

1. Centralized Management
   
2. Single Sign On
   
3. Simplified Access
   
4. Stronger Security
   
5. Standardized Administration
   
6. Simplified Deployment

<br>

####Features of Active Directory

- A set of rules, the schema, which defines the classes of objects and attributes contained in the directory, constraints placed on objects, and their naming format.
  
- A global catalog containing info about every object in the directory.
  
- It is a query and index mechanism which allows network users or applications to pull information about objects and their properties.
  
- Includes a replication service which distributes directory data across a network.
  
- Uses Lightweight Directory Access Protocol (LDAP) as an access protocol.

<br>

####Active Directory Objects

- The building blocks of an AD network.
  
- They represent a resource such as users, computers, or printers that are part of the network.
  
- Every object has a set of information detailing them, which are called attributes.
  
- There are two types of AD objects:
    1. **Container objects**: They are able to contain other objects within them.  Organizational Units (OUs) and Groups are great examples of this type of object.
       
    2. **Leaf Objects**: They cannot contain other objects but instead are representations of resources on the AD network.  Some examples are users, computers, and printers.

<br>

####Active Directory Object Classes

- Object Classes are part of the schema.
  
- They are a template for the objects and define the attributes that each object should have.

- There are three types of object classes:
  1. **Abstract class**: A top-level class that contains other abstract or structural classes. It defines only the basic attributes of an object.
  2. **Structural class**: The main component that defines an object and what attributes it should have. A structural class always comes under an abstract class or another structural class.
  3. **Auxiliary class**: They contain additional attributes which other classes can inherit from. Normally, these attributes are the ones that other classes don't define, but can inherit when necessary.  They are able to be sub classes of an abstract class or another auxiliary class.
<br>

####Active Directory Structure

- Active Directory is a hierarchical structure of Active Directory domains and organizational units (OUs) in a forest.
  
- A **forest** is the highest level of the logical structure and is a collection of one or more domain trees.
  
- A **domain** is a logical grouping of objects on a network.  They are created to establish administrative boundaries between different network entities.
  
- **Organizational Units (OUs)** are containers within a domain that are used to group resources for management purposes such as applying Group Policy or delegating control to administrators

<br>

####Other Key Terms

- **Rights and privileges**: System-wide capabilities that are granted to security principals such as users, services, computers, or groups.

- **Permissions**: Access controls that are applied to securable objects such as the file system, registry, service, and Active Directory objects.

- **Group Policy**: An infrastructure that allows specific configurations to be implemented for users and computers.  It is used to manage security settings such as password policy, user rights assignment, audit policy, registry values, file and registry ACLs, and service startup modes

- **Group Policy Object (GPO)**: is a virtual collection of policy settings.  It has a unique name, such as a GUID

- **Schema**: Contains definitions for all the objects in the directory and how they relate to each other.  There is one schema per forest and a copy of this schema exists on every domain controller in the forest.

- **Active Directory User Accounts**: Provide important information as to what resources and which files and folders a user can access.

- **Local User Account**: Exists only in the System Account Manager (SAM) database of the host computer.

- **Domain User Account**: Allows users to log on to the network using Single Sign-On (SSO) credentials stored in Active Directory.

<br>

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

<br>

###Active Directory Privileged Groups
Accounts in the Domain Admins, Enterprise Admins, and built-in Administrators groups are the most targeted by attackers.

<br>

####Enterprise Admins (EA)

- A group that exists only in the forest root domain, and by default, it is a member of the Administrators group in all domains in the forest.
  
- EA's are granted rights and permissions that allow them to affect forest-wide changes.
  
- Membership in this group is only required when first constructing the forest or when making certain forest-wide changes.

<br>

####Domain Admins (DA)

- A group which is on every domain in a forest and for which members in this group have domain-wide privilege.
  
- They are all-powerful within their domains.  
  
- Is a member of its domain's Built-In Administrators (BA) group and is a member of the local Administrators group on every computer joined to the domain.
  
- DA membership should only be required if an account with high levels of privilege on every computer in the domain is needed or certain domain wide changes must be implemented.
<br>

####Built-In Domain Local Administrators (BA)

- A group for which Domain Admins and Enterprise Admins are nested. Members are granted many of the direct rights and permissions in the directory and on domain controllers.
  
- This group is granted full control permissions on most directory objects and can take ownership of directory objects.
  
- Much of the power of the EA and DA groups are actually "inherited" from their membership in the BA group.

<br>

####Schema Admins (SA)

- Exists only in the forest root domain and has only that domain’s built-in Administrator account as a default member.
  
- Although more restricted in its capabilities than the other privileged groups, if abused, it can still damage or destroy an entire Active Directory forest.

<br>

####Securing Privileged Groups

1. Using privileged accounts to browse the internet should be forbidden.
   
2. When highly privileged accounts are used, they should only be on designated, secure systems such as domain controllers or secure administrative hosts.
   
3. In order to reduce the attack surface, Microsoft recommends that membership in the EA, DA, and BA groups should be reduced to the smallest number of accounts possible

<br>

