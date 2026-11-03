# H2 - Scene

## Part A: Covert Access Team Podcast - Myths of high security buildings

The podcast episode discusses myths related to high-security buildings. High-security buildings are often associated with expensive security technologies such as surveillance cameras, access control systems, biometric authentication, reinforced walls, and high perimeter fences. However, modern security equipment alone is not sufficient to prevent unauthorized access to facilities.

### Security Myths

* More cameras mean better security: Not necessarily. Cameras must function as intended and be integrated into an effective monitoring process. Any detected event should trigger an alert that is consistently reviewed and acted upon. It is also important to recognize that false alarms can be generated intentionally to divert attention or overwhelm security personnel. In addition, appropriate retention periods for video recordings should be carefully considered.

* Locks and sensors improve security: While locks and sensors are important security measures, building exits must also be considered. In many cases, people can exit a building without a key or access credential. For example, motion sensors may automatically unlock doors when someone is leaving a space. These sensors can sometimes be manipulated, allowing a door to be opened from the wrong side and potentially enabling unauthorized entry.

* Audits ensure security: Audits often focus on verifying whether specific security controls and procedures have been implemented. However, they do not always evaluate security from the perspective of an intruder, which may leave exploitable weaknesses undiscovered.

* Routine inspections improve security: Regular testing of door locks and alarm systems is important, but these activities can sometimes introduce vulnerabilities. For example, doors may inadvertently be left unlocked or alarm systems temporarily disabled during testing and maintenance procedures.

* Access cards improve security: The risk often increases as the number of employees in a building grows. People may not pay attention to whether someone is carrying an access card or whether the card is valid for the area. Unauthorized individuals may gain entry simply by following an employee into the area while appearing to belong there, for example by talking on a phone and carrying a coffee cup.

* Facility maintenance personnel: Maintenance staff may have extensive access rights throughout a building and can move freely in areas when other employees are not present. Cleaning and maintenance activities are often performed during evenings or outside normal business hours, which can create additional security considerations.

The podcast episode emphasizes the role of people in security, highlighting that humans are often the weakest link. According to the interviewee, something as simple as being friendly and approachable can encourage employees to provide assistance, such as holding doors open or granting access. Valuable information may also be unintentionally revealed during casual conversations or by overhearing discussions between employees.

In my opinion, the podcast presented several insightful observations that I have also encountered in working life. Technical weaknesses are often relatively easy to identify, but employee behavior and security awareness frequently require additional guidance and training. Even as a visitor, it is often possible to move around different companies' premises without being challenged, provided you appear confident and act as though you know what you are doing.


## Part B: Blog

ChainDrop: Inside a Self-Propagating npm Worm

Paloalto cybersecurity unit called Unit 42 published reserch article about malware which had infected nearly 500 NPM packages. Node Package Manager (NPM) is a packege manager JavaScript environment Node.js. NPM is a software registry and code repository for pre-build JavaScript packages for server-side and frontend projects. Infected packages work as expected and user may not notice anything. 

One sign of the infection is package.json file containing call to preinstall node_setup.mjs file pointing to setup.mjs which checks if Bun package is installed, and then injects JavaScript payload math_init.js. 

### Malware behavior

* Uses Ethereum blockchain smart contracts for command-and-control
* Steals credentials, tokens and keys (Git, SSH, Vaults)
* Steals configuration files, shell history, Bitcoin and Electrum wallets and more
* Spreads by committing modified versions versions of packages it can access 
* Gains persistence on users workstation by autolaunching when VS Code project is opened or when starting Claude Code session
* Malware also carries an installer for macOS and Linux, but it's missing a start routine.

### Detection and mitigation

* Identify and remove any affected package versions
* Investigate workstations for signs of the worm presense
* Check for unexpected NPM publishing and GitHub repository activity
* Revoke and rotate credentials
* Block any communication channels used by the worm

According to the information provided in the article, the malware is not technically difficult to remove, but its potentially widespread distribution makes the process labor-intensive. In addition, any data that may already have been compromised or leaked will require further mitigation measures.

## Part C: Science that

### A Review of Malware Analysis Techniques: Static, Dynamic, Forensic, and
Hybrid Approaches

I did some comparison about technologies introduced in blog about ChainDrop worm. Here are some that were discussed in both of the articles.

* Obfuscation of the payload
* Encryption
* Machine learning models and analysis Techniques
* Memory analysis
* Command-and-control protocols (C2)


## Part D: Download debian 13-trixie

## Part E: Install debian on virtual machine

## Part F: Install feed reader

## References

Terokarvinen.com CyberSecurity - https://terokarvinen.com/cyber-security/#homework

Covert Access Team Podcast - Myths of high security buildings - https://www.youtube.com/watch?v=fqOX3PrQ94k

ChainDrop: Inside a Self-Propagating npm Worm - https://unit42.paloaltonetworks.com/chaindrop-npm-worm-analysis/

https://ijimas.org/wp-content/uploads/2025/09/Malware-Analysis-Techniques.pdf

A Review of Malware Analysis Techniques: Static, Dynamic, Forensic, and
Hybrid Approaches - https://ijimas.org/wp-content/uploads/2025/09/Malware-Analysis-Techniques.pdf

