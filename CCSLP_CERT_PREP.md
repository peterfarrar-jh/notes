<div>
    <style>
        .wrapper {
            margin: 0 auto;
            display: flex;
            flex-direction: row;
        }
        .content-wrapper {
            border: 2px solid grey;
            margin: 1rem;
        }
        .content-wrapper.two {
            width: 50%;
        }
        .content-wrapper.three {
            width: 33.3%;
        }
        .list-wrapper {
            border: none;
            margin: 0 1rem 1rem;
        }
        .list-wrapper.two {
            width: 50%;
        }
        .list-wrapper .invisible {
            list-style-type: none;
        }
        .heading {
            padding: 1rem 0 1rem 0;
            font-weight: 700;
            text-align: center;
            color: #3486eb;
            text-decoration-line: none;
        }
        .space {
            height: 1rem;
        }
        .center {
            text-align: center;
        }
        .content {
            padding: 0 1rem 1rem;
        }
        .gold {
            background-color: #ebb61a;
        }
        .aqua {
            background-color:rgb(57, 208, 165);
            padding: .5rem 1rem;
        }
        .blue {
            background-color: #498ceb;
        }
        .plumb {
            background-color:rgb(157, 73, 235);
        }
        .deep-grey {
            background-color:rgb(104, 103, 103);
        }
        .light-grey {
            background-color:rgba(210, 210, 210, 0.81);
        }
        .small-circle {
            border-radius: 1rem;
            height: 2rem;
            width: 2rem;
            text-align: center;
            padding: .125rem;
            font-weight: 700;
        }
        .small-circle.center {
            margin: -1.25rem auto .25rem auto;
        }
    </style>
</div>

# Domain 1: Secure Software Concepts
### Secure software concepts
12% of the exam  
#### Core Concepts
* Confidentiality, integrity, and availability
* Authentication and authorization
* Accountability and nonrepudiation

#### Security Design Principles
* Access controls
* Pricples of least privilege
* Separation of duties
* Resiliency
* Economy of mechanism

#### Layerd Controls
* Defense in depth
* Diversity of defense
* Component reuse
* Least common mechanism

#### Additional Concepts
* Open design
* Psychological acceptability

### What you should know
<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Dynamic Application<br />Security Testing</div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Static Application<br />Security Testing</div>
            <div class="space"></div>
        </div>
    </div>
</div>

#### Complementary courses on LinkedIn by Jerod Brennen:  
Dynamic Application Security Testing with Jerod Brennen  
Static Application Security Testing with Jerod Brennen  

### The goals of application security
Video Gamese
Critical Infrastructure
Automobiles
Personal Information
Healthcare Data
Application Security

<div>
    <h3>Information Security Domains</h3>
    <div class="wrapper">
        <div class="list-wrapper two">
            <ul>
                <li>Applications</li>
                <li>Endpoints</li>
                <li>Networks</li>
                <li>Servers</li>
            </ul>
        </div>
        <div class="list-wrapper two">
            <ul>
                <li>Data</li>
                <li>Locations</li>
                <li>People</li>
                <li class="invisible"></li>
            </ul>
        </div>
    </div>
</div>

## The CIA Triad
Named after the three componants in the triad:
* Confidentiality
* Integrity
* Availability

### Confidentiality
Keeping secrets secret  

<div>
    <div class="wrapper">
        <div class="content-wrapper three">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Benefits</div>
            <div class="content center">Actively being accessed by users</div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle blue center">2</div>
            <div class="heading">Benefits</div>
            <div class="content center">Structured data stores<br />Unstructured data stores</div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle plumb center">3</div>
            <div class="heading">Benefits</div>
            <div class="content center">Wired networks<p />Wireless networks<p />Mobile networks</div>
        </div>
    </div>
</div>

_Data can be in the three states: in use in the app, in a data store, or in motion between the app and a data store._  

&nbsp;  

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Structured</div>
            <div class="content center">Full disk encryption (FDE)<br />File encryption<br />Data element encryption</div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Unstructured</div>
            <div class="content center">Transparent database encryption (TDE)<br />Column-level encryption<br />Field-level encryption</div>
        </div>
    </div>
</div>

_Data stores come in two flavors._  

#### Encryption in Motion
* Secure Sockets Layer (SSL) certificates
* Transport Layer Security (TSL) certificates
* Virtual private networks (VPN)

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Overt</div>
            <div class="content center">Unhidden channel (for example, TLS-encrypted web application)</div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Covert</div>
            <div class="content center">Hidden channel<br />(for example, steganography)</div>
            <div class="space"></div>
        </div>
    </div>
</div>

_It's a good idea to be overt about encryption if you want the user to have confidence in the application._  

#### Data Flow Diagram (DFD)
Tracks how an application processes, stores, and transmits data, including how data is protected both in motion and at rest (for example, network protocols, encryption algorithms)  

### Integrity
_Security is ultimately about trust._  

#### Integrity
Protecting data from unauthoried changes 

Often accomplished by comparing a given value to a value the app knows to be true.  

#### Hashing
* Type of cryptography
* Converts data to text string
* Can't be reversed (ideally)
* Can be reproduced

#### Digital Signatures
* Applied to messages and documents
* Asymmetric encryption (public/private keypair)
* Prove sender's identity

#### Code Signing
* Digital signature for executables
* Verify the author's identity
* Verify that the code hasn't been modified

#### Purpose of Integrity Controls
* Guarantee authenticity
* Guarantee reliablility

### Availability
_Ensuring that the application meets its availability requirements._  

#### Availability
The app is there when users expect it to be.  

Something as simple as an expired SSL certificate can cause a web application to fail, and potentially cause harm to an organization's income, and reputation.  

#### Enabling Availability
* Redundancy
* Replication
* Clustering

At some point, your application is _going_ to break.  

Redundancy means there is another version of the app ready to spin up if the running version fails (failover).  

Replication means multiple versions of the application are running, and user data is being copied (replicated) to those other instances (notes).  

Clustering means tieing systems all together. One component monitors systems and directs traffic to available nodes.  

#### Why Availablity Matters
* Enables scalability
* Enables resiliency

This is good for business.  

## Identity and Access Management
### Authentication
_We don't want to give just anyone access to our data._  

#### Authentication
Prove you are who you say you are  

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Identity Management</div>
            <div class="content center">All the accounts tied to an individual user</div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Access Management</div>
            <div class="content center">What the user can do with all those accounts</div>
            <div class="space"></div>
        </div>
    </div>
</div>

There are three types of IAM events that the app needs to know about.  

#### Joiners
When the relationship with the application begins. New hire.  
#### Movers
Something has changed. Sebaticals, promotions, etc.  
#### Leavers
Someone leaves. Termination, resignation.  

Traditional user name password controls are no longer considered strong authentication

#### Strong Authentication
* Comnplex passwords
* Two-factor authentication
* Multifactor authentication

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Two Factor</div>
            <div class="content center">Username, password, and one additional factor of authentication</div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Multifactor</div>
            <div class="content center">Username, password, and one <strong>or more</strong> additional factors of authentication</div>
            <div class="space"></div>
        </div>
    </div>
</div>

Often used interchangably, they are slightly different. "Two Factor" auth is a subset of "Multi Factor" auth. Secret tokens, digital certificates, location data, biometrics.   

#### Single Sign-On (SSO)
* User logs in once
* All other authentication occurs automatically

#### Federated Identity
* Spans multiple organizations
* Identity provider (IdP) + Service provider (SP)
* Security assertion markup language (SAML)
* OpenID
* OAuth

_(Technically, OAuth is used for authorization)_  

Single sign on is great for managing passwords, and allowing all apps to use the same trusted signon mechanism, and providing a better user experience. However, if an attacker get's your password, they have access to all of your apps. MFA could help provent this. The role of the CCSLP is to balance the security needs and come up with the right mix for the organization.  

### Authorization
Granting users access to specific resources once they've authenticated to your application.  
Broken controls prevent users from using the app, or provides access to attackers.  

#### Access controls
* Subjects = users
* Objects - screens, functions, files, data elements 

&nbsp;  

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Attributes</div>
            <div class="content center">Flags or characteristics that indicate specific access controls</div>
            <div class="space"></div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Entitlements</div>
            <div class="content center">Representations of specific access</div>
        </div>
    </div>
</div>

_Administrative access is an example of an entitlement. An admin attribute can control who gets admin rights._  

#### Access Controls
* Create
* Read
* Update
* Delete


<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">RBAC</div>
            <div class="content center">
                Role-based access controls<br />Grouped based on job function
            </div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">ABAC</div>
            <div class="content center">
                Attribute-based access controls<br />Based on IF/THEN logic
            </div>
            <div class="space"></div>
        </div>
    </div>
</div>

#### Fine-Grained Authorization
Controlling access to specific forms and fields within the app  

Using attributes for each field or form, an administrator can control each of these for each user. This provides both improved security. But it also provides an improved user experience by only showing users what they need to see.  

### Accountability
"Doveryai, no proveryai.  
(Trust, but verify.)  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
 -- Russian proverb

#### Accountability
Being able to determine **who** did **what** within your app and **when** they did it  

For accountability to work, you need good logging.  
Identify your logging and monitoring requirements.  

#### Auditing
The _process_ of going back to determine **who** did **what** within your app and **when** they did it  

_External standards and regulations can help establish logging and monitoring requirements_  
Every regulated industry has a publicly available set of security requirements.  

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Incident Response</div>
            <div class="content center">
                Short term, contain the damage
            </div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Forensics</div>
            <div class="content center">
                Long term, legal implications
            </div>
            <div class="space"></div>
        </div>
    </div>
</div>

_Logging should be set for each component of the application_  

<div>
    <h3>Logging Levels</h3>
    <div class="wrapper">
        <div class="list-wrapper two">
            <ul>
                <li>All</li>
                <li>Debug</li>
                <li>Info</li>
                <li>Warn</li>
            </ul>
        </div>
        <div class="list-wrapper two">
            <ul>
                <li>Error</li>
                <li>Fatal</li>
                <li>Off</li>
                <li>Trace</li>
            </ul>
        </div>
    </div>
</div>

#### Factors to Consider
* Cost of storage (retention)
* Review capabilities
* Standards and regulations
* Data classification
* Application criticality

### Nonrepudiation
_Applications can have financial and legal implications. How do you know the person on the other end is really who they say they are?_  
_Digital signatures are the most common tool for non-repudiation_  

#### Digital Signature
An encrypted value generated with an individual's private key, used to prove the identity of the sender  

#### Public Key Infrastructure
All the people, processes, and technologies that you use to issue and manage digital certificates (for example, X.509)  

Sender uses their private key to generate a signature. The recipient uses the senders public key to verify the signature. This is the opposite of encrypted file exchange, where the sender uses the recipients public key, and the recipient uses their private key to decrypt.  

#### Blockchain
Collection of digital records that are encrypted and connected to one another using cryptography  

_With blockchain, each block contains a cryptographic hash of the previous one._  

### Governance, risk, and compliance
<div>
    <div class="wrapper">
        <div class="content-wrapper three">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Governance</div>
            <div class="content center">
                Written artifacts that support your application security program
            </div>
            <div class="space"></div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle blue center">2</div>
            <div class="heading">Risk (Management)</div>
            <div class="content center">
                Threat, vulnerabilities, likelihood, and impact
            </div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle plumb center">3</div>
            <div class="heading">Compliance</div>
            <div class="content center">
                Regulations, lasw, and industry standards
            </div>
        </div>
    </div>
</div>

_Building all three into the security program makes the program more efficient._  

_If you don't tie these three programs together, you'll likely find your program drifts in the wrong direction._  

#### Unified Compliance Framework
* https://www.unifiedcompliance.com/
* Over 800 authority documents
* Appointed by government entities
* For example: SEC, FTC, EPA
* Standards-setting bodies: PCI

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Legal</div>
            <div class="content center">
                Potential fines and/or jail time
            </div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Industry</div>
            <div class="content center">
                Loss of privilege to participate in a given industry
            </div>
            <div class="space"></div>
        </div>
    </div>
</div>

Example of legal compliance: Sarbanes-Oxley act (2002)  
Eample of an industry standard: PCI (credit card standard)  

## Access Controls
Convenience vs. Security.  

### Least privilege
#### Principle of Least Privilege  
Giving people the right amount of access they need (and nothing more) so they can do their jobs  

Organizations change over time. Early employees are typically over entitled. New users are given permissions based on existing profiles, so they may be duplicating these over entitled users and violating the principle of least privilege.  

<div>
    <div class="wrapper">
        <div class="content-wrapper three">
            <div class="small-circle aqua center">1</div>
            <div class="heading">MAC</div>
            <div class="content center">
                Mandatory access control
            </div>
            <div class="space"></div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle blue center">2</div>
            <div class="heading">DAC</div>
            <div class="content center">
                Discretionary access control
            </div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle plumb center">3</div>
            <div class="heading">NDAC</div>
            <div class="content center">
                Nondiscretionary access control
            </div>
        </div>
    </div>
</div>
All work within the RBAC model  

#### Mandatory Access Control
* Data classification (objects)
* Clearance (subjects)
* Need-to-know

#### Discretionary Access Control
* Resource owner
* Identity based
* RBAC to scale

#### Nondiscretionary Access Control
* Takes the humans out of the equation
* Policy is policy
* All or nothing

#### Run-Time Privilege
Access rights are escalated and de-escalated each time a process is executed.  

#### Zero Trust
* Validate each access request.
* Never trust, always verify.

### Seperation of duties
As organizations grow in size, they also grow in complexity. It may become more difficult to determine who has access to what. And so, it becomes difficult to determine if users have access they shouldn't. That risk could be mitigated using "segregation of duties" (SOD).  

#### Segregation of Duties
Dividing sensitive functions among multiple parties to reduce the likelihood that any one person has too much authority or access

_NOTE:_ People need three things to commit fraud:  
1. A motive
2. A mindset that lets them justify their actions
3. Opportunity

Opportunity can manifest itself as weak or missing access controls.  

**Invoicing** scenerio:
To keep track of money, some people approve purchase orders, and someone else pays the invoices. But what if they were the same person? They could authorize payment for things that don't exist and direct that money to themselves.  

_The Office Space Scenerio:_ What if a developer has the ability to write code, and move it into production without anyone looking at the code?    

#### Intentional or unintentional?
Say a developer finds a bug in the middle of the night that could impact the system in a negative way. They push a bug fix on their own to prevent the problem. Turns out the bug fix had an issue and it brought down the whole system while they slept. In this case, SOD can protect us from ourselves.  

#### Multiparty Control
* Determine component parts
* Two or more individuals
* Collaboration

#### Secret Sharing and Splitting
* No individual has complete control
* Encryption keys

Assign two or more administrators to manage the secrets, but only give part of the secrets to each. It will take two people to put them together.  

### Economy of mechanism
The application landscape continues to become more complex.  

_"Complexity is the worst enemy of security, and our systems are getting more complex all the time."_  
    - Bruce Schneier, _Data and Goliath: The Hidden Battles to Collect Your Data and Control Your World_  
  
The more complex an application, the more difficult it is to secure it, and the more difficult it is for end-users to follow good security procedures when using it.  

#### Economy of Mechanism
Getting rid of everything that your app doesn't need, making it easier to deploy, manage, secure, and use

Microsoft Windows has 50 million lines of code.  

#### Bypassing the iOS Lock Screen
* iOS 4.1 - emergency call
* iOS 6.1 - emergency call
* iOS 7 - control center/alarm clock
* iOS 8.1 - unlimited passcode guesses
* iOS 12 - Siri

Researcher was able to bypass the lock screen using the emergency call feature. The bug was fixed, but somehow resurfaced two versions later. Other hacks have been found, including just asking Siri for help.  

iOS has a large, complex code base, like Windows.  

Large organizations have hundreds of internal application. Each, typically, requires a username and password to keep track of. Each provides an opportunity to introduce a security flaw.  

#### Single Sign-On (SSO)
User logs in once, and then they are automatically logged in to every connected application.  

If a criminal gains access to an account with SSO, they have access to every application the user has access to. But it also makes it easier for the security team, using things like MFA or location based authentication.  

#### Password Vaults
* Encrypted credential store
* Reduces password reuse
* Protect with strong vault password
* Protect with MFA

Can create random passwords for each application that they don't have to remember themselves.  

### Complete mediation
Sensitive information leads to security needs.  

#### Complete Mediation
Check authorization every time a user or process touches an object  

Example: Monitoring web traffic for a web app, noticed a url with "user" and a number. Changed number and became a new user. Was able to gain admin access. If using complete mediation, the app would have seen the first try was not allowed and prevented the attack.  

#### Cookie Management
* Small texdt file
* Stored client-side
* Check often by the app
* Targeted by attackers

If the app continuously monitors the cookie, it should be able to catch if a user is doing something they shouldn't. And if the cookie doesn't contain what the app expects it too, it can shut down the app.  

#### Session Management
* Log in to log out
* Server checks session ID
* Server checks for active session

#### Caching of credentials
* Client-side storage
* Better performance
* Credentials expire
* Potential compromise

Caching credentials is risky  

## Design Consideration
### Defence in depth
Complex applications present a broad attack service to criminals.  
No single security control will stop all attacks.  

#### Defence in Depth
Using multipl, layered security controls to prevent, detect, and respond to potential attacks  

Compare to a middle age castle.  

#### Form Fields
* Username
* Password
* Search

Attackers are looking for ways to abuse one or more of these fields.  

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Protocol-Based</div>
            <div class="content center">
                SQL injection<br />
                LDAP injection<br />
                XML/XPATH injection
            </div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Structured</div>
            <div class="content center">
                CSRF<br />
                XSS<br />
                OS command injection
            </div>
            <div class="space"></div>
            <div class="space"></div>
        </div>
    </div>
</div>

#### Input Validation
Treating all user input as untrusted and performing some sort of check on that input before sending it to any back-end systems  

Monitoring and logging can help raise alerts that can allow actions to be taken to shut down attacks before any damage is done.  

#### Security Zones
Seperate, secure enclaves that hinder an attacker's ability to jump from a compromised system to another system on the same network  

<div>
    <div class="wrapper">
        <div class="content-wrapper three">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Public</div>
            <div class="content center">
            Anyone can access this data.
            </div>
            <div class="space"></div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle blue center">2</div>
            <div class="heading">Internal</div>
            <div class="content center">
            Only authorized users can access this data.
            </div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle plumb center">3</div>
            <div class="heading">Regulated</div>
            <div class="content center">
            Only <strong>specific</strong> authorized users can access this data.
            </div>
            <div class="space"></div>
            <div class="space"></div>
        </div>
    </div>
</div>

### Resiliency
Don't focus only on what the app is supposed to do, consider what it might do if it breaks and take steps to insure the app handles those situations gracefully.  

#### Failsafe
Elemnts we build into systems and applications so errors trigger responses that don't inadvertently expose too much information

Show the developer/admin/user just the right amount of information without exposing too much data.  

#### Exception Handling
* Server errors
* Code bugs
* Invalid input

Replace default error messages with customized error messages

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Verbose Errors</div>
            <div class="content center">
            Default behavior<br />
            Technical<br />
            Expose sensitive information
            </div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Non-verbose Errors</div>
            <div class="content center">
            Your design<br />
            User-friendly<br />
            Limit what's exposed
            </div>
            <div class="space"></div>
            <div class="space"></div>
        </div>
    </div>
</div>

Verbose error messages are great for developers debugging an application.  
Non-verbose error messages limit the ability of an attacker to use that information to further their attack.  

#### Deny by default
Don't grant access unless you're absolutely certain that everythin's working and that the user is properly authorized  

#### "Failsafe" versuse "fail safe"
Failsafe is a type of control  
Fail safe is a specific way that an app can fail  

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Fail Secure</div>
            <div class="content center">
            When things brea, the app stops working<br />
            Access to sensitive data
            </div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Fail Safe</div>
            <div class="content center">
            When things break, the app keeps working<br />
            Physical safety
            </div>
            <div class="space"></div>
            <div class="space"></div>
        </div>
    </div>
</div>

#### Failover
When the primary system or app goes down, a backup automatically takes its place.  

### Open design
"Hidden" is not secure. It is better to have as many pairs of eyes as possible looking at your code.  

#### Open Design
While some components should remain secret (like encryption keys and passwords), the overall design of a system should be known and vetted by a larger team.  

#### How secret are your secrets?

#### Reverse Engineering an Android App
* Download the .apk file to your laptop
* Import the .apk into Eclipse
* Run dex2jar against the .apk in Eclipse

#### Protect Your Secrets
* Encryption keys
* Passwords
* API keys
* Internal developer comments

Even if you think your compiled code is securly hiding your secrets... don't be too sure. Keep secrets out of your code.  

Don't be too sure encryption algorithms will keep your secrets safe either. Algorithms have a long history of being broken  

#### Peer-Reviewed Algorithms
* AES, DES, MD4, SHA-1
* Security and performance
* NIST FIPS PUB 140-3

AES, DES, MD4, SHA-1 were once thought secure.  
Be sure your algorithms are well vetted.  
NIST FIPS PUB 140-3 is dedicated to security requirements for encryption modules.  

#### Kerckhoffs' Principle
A cryptosystem should be secure even if an attacker knows everything about it (except for the key).  

<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Open Source</div>
            <div class="content center">
            Everyone in the world can access and review your code.
            </div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Crowdsource</div>
            <div class="content center">
            A select, vetted group of people can access and review your code.
            </div>
            <div class="space"></div>
            <div class="space"></div>
            <div class="space"></div>
        </div>
    </div>
</div>

Open design fosters team communication.  
Document and share your designs.  

### Least common mechanism
Reusing existing components is the norm.  

### Least Common Mechanism
Striking the right balance between when you should reuse existing components and when you should separate data and functions so you can proactively mitigate or contain potential damage  

Server admins use this mechanism  

#### What are the risks?

#### Isolation and Compartmentalization
* Identify sensitive functions
* Restrict access to certain roles
* Assume compromise

#### How to Accomplish
* Credentials and permissions
* Virtual machines
* Serverless functions
* Segmented networks

Isolating sensitive data to its own network and restricting access to that network will help achive security and compliance objectives.  

#### Allowlisting
Preapproving only those resources that an app is permitted to use  

### Psychological acceptability
You may be tempted to implement every tool you know to secure an application. Don't do that. Too much security will frustrate users.  

#### Psychological Acceptability
Considering how security will impact the users so that you don't implement controls that the users are constantly trying to circumvent  

#### Your Application Should
* Do what it was designed to do
* Provide the user with a good experience
* Protect the user and the data from harm

#### It's not about security. It's about risk.
What level of risk is the organzation willing to live with? Sometimes more risk can facilitate faster times to market. Sometimes it can provide a better user experience. Consider these risks in advance, and conciously choose how much risk to allow.  

"The more secure you make something, the less secure it becomes."  
    - Bruce Schneier

Include the users as part of the planning.  

#### CAPTCHA
**C**ompletely  
**A**utomated  
**P**ublic  
**T**uring test to tell  
**C**omputers and  
**H**umans  
**A**part  

#### Biometrics
Using physical traits to automatically verify a user's identity  

Passwordless authentication, like a finger print.  

### Leveraging existing components
Organizations tend to have a large number of components already developed over the years.  

#### Leveraging Existing
If you've already figured out how to use something, try reusing it in new apps instead of reinventing the wheel.  

#### Finding the Right Mix
* Economy of mechanism
* Least common mechanism
* Complete mediation

One size does not fit all.  

#### Benefits
* Speeds up the development process
* Existing knowledge
* Already secured
* Legacy support

#### Drawbacks
* Limits innovation
* Existing vulnerabilities
* Bound to legacy systems (tech debt)

#### Risk vs. Reward

### Eliminate single point of failure
A chain is only as strong as its weakes link.  

#### Single Point of Failure
If one specific thing breaks, it can bring down the entire app.

Ask yourself, if this one thing breaks, will it bring down the entire app? If the answer is yes, that's a _single point of failure_.  

#### Confidentianality Failures
* Weak authentication mechanisms
* Weak authorization mechanisms
* Unencrypted sensitive data
* Plaintext credentials

#### Integrity Failures
* No principle of least privilege
* No separation of duties
* Unpatched technical vulnerabiliities

#### Availability Failures
* Denial of service conditions
* Insufficient resources
* Unreliable components

Plan to fail.  
Failure is part of the process.  
That's okay.  
Plan for failures ahead of time and design the app accordingly.  

<div>
    <div class="wrapper">
        <div class="content-wrapper three">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Confidentialtiy</div>
            <div class="content center">
            Multifactor authentication<br />
            Encryption/hashing Access controls
            </div>
            <div class="space"></div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle blue center">2</div>
            <div class="heading">Integrity</div>
            <div class="content center">
            Principle of least privilege<br />
            Separation of duties<br />
            Vulnerability management
            </div>
        </div>
        <div class="content-wrapper three">
            <div class="small-circle plumb center">3</div>
            <div class="heading">Availability</div>
            <div class="content center">
            Failover<br />
            Backups Load balancing
            </div>
            <div class="space"></div>
            <div class="space"></div>
            <div class="space"></div>
        </div>
    </div>
</div>

### diversity of defense
Multiple defenses are more likely to ward off an attack

#### Geographical Diversity
* Promarily an availability control
* Multiple physical locations
* Infrastructure-as-a-service (IaaS) providers
* Achieve resiliency
* Backup and recovery

#### Technical Diversity
* Keep to a minimum
* Low complexity for developers
* High complexity for attackers
* Effective against reverse engineering

Excessive diversity in technology can make it difficult to find engineers capable of managing them all. Using multiple languages can provide protection against attackers who may be trying to reverse engineer the application. C is particularly good for this.  

Too much diversity can be expensive and hard to maintain. Not enough may make it too easy for attackers to compromise the application.  

#### Distributed Systems
Multiple components on different machines all working independently even though it feels like a single system to the user  

# Domain 2: Secure Software Lifecycle Management
### Secure Software Lifecycle Management

Securly managing deployed software all the way through to its eventual decommission.  
11% of the CSSLP exam.  

#### Configuration and Version Control
* Hardware
* Software
* Documentation
* Interfaces
* Patch management processes

#### Lifecycle Management Strategy
* Roadmap integration
* Adaptive versus predivtive methodologies
* Unique security considerations

#### Standards and Frameworks
* Popular security frameworks
* Impact on security documentation

#### Security Metrics
* Defects per line of code
* Criticality levels
* Remediation time
* Software complexity

#### Status Reporting
* Engaging stakeholders
* Reports
* Dashboards
* Feedback loops

#### Securely Decommission Software
* End-of-life policies
* Retention requirements
* Other dependencies

#### integrated Risk Management (IRM)
* Regulation requirements
* Compliance requirements
* Legal requirements
* Maturity models
* Technical versus business risks

#### Security Culture
* How to promote
* Continuous improvement processes

## Laying Your Foundation
First, lay out a plan: 
* Strategy
* Roadmap

#### Software Development Life Cycle
Often represented as a circle, because every step leads back to the begining:  
Design -> Implementation -> Testing -> Deployment -> Maintenance -> Analysis -> Design  

#### Control Gate
A logical or technical control that makes sure code quality meets standards at every stage of the SDLC  

#### Break/Build Criteria
Specific measurements used to determine if a build can proceed or if the code needs to be fixed  

#### Product Road map
A documented plan for projecting and tracking how your apps will change over time  

Road maps are often tracked and updated on a quarterly basis.  

Security strategy need to be aligned with the same roadmap.  

#### External Facotrs
* Standards, regulations, and legal requirements
* Customers and partners expectations
* Platform integration (APIs)
* Cloud adoption

Understand how all these factors might impact the product road map and engage with the product owner to insure that the security strategy and the product strategy go "hand in hand."  

### Development methodologies
<div>
    <div class="wrapper">
        <div class="content-wrapper two">
            <div class="small-circle aqua center">1</div>
            <div class="heading">Predictive</div>
            <div class="content center">
            Plan everything ahead of time
            </div>
        </div>
        <div class="content-wrapper two">
            <div class="small-circle blue center">2</div>
            <div class="heading">Adaptive</div>
            <div class="content center">
            Change as you go
            </div>
            <div class="space"></div>
            <div class="space"></div>
            <div class="space"></div>
            <div class="space"></div>
        </div>
    </div>
</div>

Example of predictive development methodologies: Waterfall  
Requirement Analysis -> System Design -> Implementation -> Testing -> Deployment -> Maintenance  
Example of adaptive development methodologies: Agile
Design -> Developmnet -> Test  
Adapt as needed  

#### Which one is right for your organization?
Small well defined projects may run smoother using Waterfall  
Large complex applications may benefit from Agile  

#### Other Development Methodologies
| Predictive | Adaptive |
|---|---|
| Prototype | Scrum |
| | Kanban |
| | Spiral |
| | DevOps |


## Setting Expectations
## Improving Over Time
# Domain 3: Secure Software Requirements
## Security Requirements
## Privacy Requirements
## Data Classification Requirements
## Validating Your Requirements
# Domain 4: Secure Software Architecture and Design
## Threat Modeling
## Security Architecture
## Security Design
## Modeling
# Domain 5: Secure Software Implementation
## Secure Coding Practices
## Finding and Fixing Vulnerabilities
## Component Security
# Domain 6: Secure Software Testing
## Developing ecurity Test Cases
## Developing a Testing Strategy
## Conduction Security Tests
## Reviewing the Results
# Domain 7: Secure Software Deployment, Operations, and Maintenance
## Deploying Your Software
## Shifting Into Operations
## Maintaining Your Software
# Domain 8: Secure Software Supply Chain
## Supply Chain Risk Management
## Ensure Software Security
## Get It In Writing

### Exam Logistics
### Conclusion
