# Module 1
### CIA
- Confidentiality:
  - Access to systems or data is limited to authorized parties
- Integrity:
  - You get "right data when asking
- Availability:
  - The system or data is there when you want it
- Privacy:
  - **information self-determination**. control information about you

### Threats
1. Interception
2. Interruption
3. Modification
4. Fabrication

### Defence
1. Prenvent it:
  - prevent the attack
2. deter it:
  - make attack harder more expensive
3. Deflect it:
  - make youtself less attractive
4. Detect it:
  - notice attack is occurring
5. Recover from it:
  - mitigate the attack effects
  
*principle of Easiest Penetration*:  system is only as strong as its weakest link  
*principle of Adequate Protection*:  security is economics

### Defence of computer system
1. Cryptography
  - make data unreadable
  - authenticating user with digital signatures/ transactions withcryptographic protocols
  - ensuring integrity of stored data
  - make personal information automatically unreadable after certain length of time
2. Software control
  - passwords and other forms of access control
  - OS separate users' action
  - Virus scanner watch for malware
  - development controls enforce quality measure on original source code
  - personal firewalls
3. Hardware control
  - fingerprint reader
  - smart tokens
  - firewall
  - intrusion detection system
4. Physical controls
  - lock
  - guard
  - off-site backup in safe place
5. Policies and procedures
  - rules about changing pasword
  - employee connects his own Wi-Fi access point to the internal company network can be attacked

# Module 2
Hard to write secure programs:  
  - Programs have bugs
  - security-relevant programs have security bugs

Flaw: **faults** and **failures**  
  1. *patching*
    - causing a narrow focus on oberved failure, instead of a broad look at what may be a more serious underlying problem
    - fault may have caused other unnoticed failures and partial fix may cause inconsistencies or other problems
    - may introduce new faults
  2. Fuzzing
    - automated tools understand common problems in system/code
    - Brute-force badinput
    - used to identify faults early
    - construct state machine and deviate from normal state flow

### Malicious flaw & nonmalicious flaw
eg: Hearbleed Bug & Apple's SSL/TLS Bug

## Vulnerability
### Buffer overflow
- off-by-one:  overwrite last bit of ebp
- overflow heap insteado f stack
- jump to parts of the program or standard libraries

Integer overflow: make signed integer wrap and become negative usually violate assumption

#### Defend buffer overflow
- use language with bounds checking
- Non-executable stack (writable or executable)
- stack at random virtual address
- "Canaries" detect if stack has been overwritten
### Format String
- %s likely crash program
- %x dump the stack
- %n write to an address on stack
### Incomplete mediation
- occurs when application accepts incorrect data from the user
- make sure user-supplied input falls within well-specified values, known to be safe

#### Client-side mediation
- JS run validation check for invalid data
- Problems: user edit form, turn off JS or connect to server manually.

#### Defend incomplete mediation
- do server-side mediation
- always do checks on values of all field
- make sure client has not modified the data

### TOCTTOU error
The state of the system changed between the check for permission and the execution of the operation
#### Defend TOCTTOU error
- make sure all information relevant to teh access control decision is constant between the time of the check and the time of the action
- keep a private copy of the request itself so the request can't be altered during the race
- act on object itself not on level of indirection
- use locks to ensure object is not changed

## Malware
software written with malicious intent  
usually needs to be executed in order to cause harm (user action, exploiting flaw in system)

### Virus
kind of malware infects other files usually executable programs.
virus want to modify an existing programs or documents that executing pr opening it will transfer  control to the virus  
Spread by sharing infect file around or p2p network  
**Payload**: malicious behavior (erase hard drive, corrupt files, etc)
### spot virus
- Signature-based protection
  - keep a list of all known viruses
  - use signature to identify
  - Problem: virus are polymorphic
- behavior-based protection
  - look for suspicious pattern of behavior
  - false negative & false positive (base rate fallacy)

### Trojan horse
program claim to do something innocuous but hide malicious behavior which user want to run  
Spread rely on multiple users executing the "trojaned" software  
usually with scareware or ransomware inside  
### Logic bomb
malicious code hiding in the software already on computer  
usually written by "insider" and meant to be triggered sometimes  
has trigger respond to sepcific events  
#### spoting Trojan & logic bomb
tricky, since user is intentionally running the code and logic bomb is part of the software already install on the computer

### Worms
self-contained piece of code can replicate with little or no user involvement  
use security flaws in widely deployed software as a path to infection  
eg. Morris, Code Red, Slammer, Stuxnet, Flame

## Malicious code

### web bug
object embedded in a web page is fetched from a different server from the one that sered the web page itself  
information of you can be sent to thrid parties without your knowledge or consent

### Back door
set of instructions designed to by pass the normal authenticaton mechanism and allow access to he system to anyone who knows it  (usefule for debugging the system, forget to take out...)  
e.g. sendmail, Code Red plant back door, Port knock

- forget to remove
- intentionally leave them for testing purpose
- for maintenance purpose (service technician)
- for legal reason (Lawful Access)
- for malicious purpose

### Salami attack
made up of many smaller, inconsequential attacks  
e.g. send the fraction of cents of round-off error from many acounts to a single account

### Privilege escalation
occurs when part of the system that legitimately runs with higher privilege can be tricked into executing commands on behalf of the attacker (buffer overflow in setuid programs or network deamons)  
attacker trick the system into thinking he is a legitimate higher-privileged user ("-froot" attack)

### Rootkits
a tool with method gaining unauthorized root / administrator privileges account, or remotely then hide itself (modify ls, ps)

### keystroke logging
- application-specific logger:
  - record onlt those keystrokes associated with a particualr application
- System keyboard logger:
  - record all keystrokes that are pressed(or only for one particular user)
- Hardware keyboard logger:
  - piece of hard ware that sits between the keyboard and computer

### interface illusion
malicious code make "nonstandard" user interface elements
e.g. phishing

### man-in-the-middle attack
keyboard logging, interface illusion and phishing are all man-in-the-middle attacks  
intercepts the communication from the user and passes to the inteded other party  

## Nonmalicious flaws

### Covert channels
capability to transfer sensitive/unauthorized information through a channel that is not supposed to transmit information  

### Side channels
learn information about what the computer is doing by looking at:
  - RF emission
  - poser consumption
  - audio emission
  - CRT reflected light
  - Reflection of screen
  - Shared CPU cache

## Software lifecycle
- Specification
- Design
- Implementation
- Change management
- Code review
- Testing
- Documentation
- Maintenance
### Security control in Design
- Modularity
  - break problem into small pieces
  - easy to check each piece for flaws, test, maintain, resuse, etc
  - need low coupling
- Encapsulation
  - modules mostly self-contained sharing information only as necessary
  - reduce coupling
  - developer should not need to know how a different module is implemented
- Information hiding
  - internals of one module should not be visible to other modules
  - prevent accidental reliance on behavior not promised in API
  - hinder malicious actions
- Mutual suspicion
  - module check input are sensible before acting
  - defence against flaws or malicious behavior on other modules
- Confinement
  - confine potentially untrustworthy module first
### Security control in Implementation
- Don't use C
- Static code analysis
  - software help find security flaws
- Formal methods
  - try to prove the code does excatly what is supposed to do
  - have to  "mark up" code with assertions or other hints to the theorem proving program
- Genetic diversity
  - many machines running the same vulnerable code
  - different HTTP server will mitigate attack
### Security control in Change management
- track changes to either the source code or the configuration information (Version Control)

### Security control in Code review
- most effective way to find faults
- Guided
  - author explains the code
  - justifies why it was dones this way instead of others
  - useful for changes to code
  - important for safety-critical system
- "Easter egg"
  - insert intentional flaws
  - more likely to find unintentional flaws

### Security controls in Testing
- make sure the implementation meets the specification
- make program do unspecified things by doing unusual thing (more like black-box)
- make program do unspecified things by taking into account the design and the implementation (white-box)
- Black-box : test where you jsut have accessto a completed object (Fuzz test)
- White-box : test conformance to a specification by taking into account knowledge of the design and implementation (useful for regression testing)

### Security controls in Documentation
- write down the choices been made
- things didn't work
- checklist of things to be careful of

### Security control in Maintenance
- organization have rules about how thing are done at each stage of software lifecycle (standards)
- make formal processes specifying how each of these standards should be implemented
- have audit comes in and verifies that processes properly

# Module 3
## Separation
- Physical
  - use different physical resource for different user
  - easy to implement expensive and inefficient
- Temporal
  - execute different users' program at different time
- Logical
  - user is given impression no other user exists
  - done by OS
- Cryptographic
  - Encrypt data make it unintelligible to outsiders
  - complex

## Sharing
OS should allow flexible sharing

## Memory and address
prevent one program from corrupting other programs or data, OS  
Memory protection is part of translation form virutal to physical address (MMU)

- Fence register
  - exception if memory access below address in fence
  - protects OS from user program
  - Single-user OS
- Base/bound register
  - Exception if memory access below/above address in base/bounds
  - different values for each user program
  - maintain by OS during context switch
  - limited flexibility
- Tagged architecture
  - Each memory word has one or more extra bits identify access right to word
  - flexible
  - large overhead
  - Difficult to port OS from/to other hardware architecture
- Segmentation
  - multiple address space (segments)
  - Different segment for code, data and stack
  - OS map from segment name to its base physical address in Segment Table
  - keep protection attributes

  **Advantages:**  
  * Each address reference is checked for protection by hardware 
  * Many different classes of data items can be assigned different levels of protection 
  * Users can share access to a segment, with potentially different access rights
  * Users cannot access an unpermitted segment

  **Disadvantages**  
  * External fragmentation 
  * Dynamic length of segments requires costly out-of-bounds check for generated physical addresses 
  * Segment names are difficult to implement efficiently

- Paging
  - program is divided into equal-sized chunks (pages)
  - Physical memory is divided into equal-sized chunks (frames)
  - Frame size = page size
  - keep memory protection attribute

  **Advantages:** 
  * Each address reference is checked for protection by hardware 
  * Users can share access to a page, with potentially different access rights 
  * Users cannot access an unpermitted page 
  * Unpopular pages can be moved to disk to free memory 

  **Disadvantages:** 
  * Internal fragmentation 
  * Assigning different levels of protection to different classes of data items not feasible 

- x86 architecture
  - both segmentation and paging
  - memory protection bit indicate no access, read/write access or read-only access
  - No execute bit

## Access control matrix
- access control list
  - column-wise
  - each object has list of subjects and their right
  - set of allowed user per object is quick
- capabilities
  - row-wise
  - unforgeable token gives owner some access right to an object
  - enforced by OS store and maintain tokens or cryptographic
  - token are transferable
  - combined usage of ACL and cap.
