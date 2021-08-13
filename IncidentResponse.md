#TODO : la mise en forme

# Getting the investigation started on the right foot
## Incident Summary Checklist
- Record date and time the incident was reported.
- Contact information of the person documenting this information.
- Contact information of the person who reported the incident.
- Contact information of the person who detected the incident.
- The nature of the incident (What was detected, mass malware, spear phishing attempt, failed logins, unauthorized access..).
- Type of affected ressources (details on the data or resources that may have been affected). -> that help to define scope.
- How the incident was detected (provide a bried summary of what the detection method was (AV,IDS or user or smthg else)).
- List computers affected by the incident (location, ip address, hostname)
- Who accessed the systems since detection.
- Who is aware of the incident.
- Whether the incident is currently ongoing.

## Incident Detection Checklist
- Was the detection through an automated or manual process ? Did a person or an automated system detect the incident ?
- What information was part of the initial detection (if it's an alert, copy of the alert or if it's from a person, what they saw)?
- What sources provided the data that contributed to the detection ? (note the timezone).
- Has someone acquired and validated that the source data is accurate ? if so, who ?
- Is the source data involved being preserved ?
- How long have the detection sources been in operation ? (May be false positive)
- What are the detection and error rates (May someone did updates recently..) ?

## Collect Additional Details
### Individual System Detail :
- Physical location : information that someone outside of your organization would be able to clearly determine where a system is located.
- The asset tag number.
- System's make and model.
- Which O.S installed.
- Primary function of the system.
- The rsponsible system administrator or user of this computer (need to be informed of what is going on).
- The assigned IP address.
- The hostname and domain.
- The critical information stored on the system.
- Whether backups exist for the system.
- Whether the system is still connected to the network.
- A list of malware detected from the time of your investigation back to the beginning of log data.
- a list of any remediation steps that have been taken.
- If any data is being preserved, what process is being used and where it is being stored.

### Network details :
- A list of all external malicious IP addresses or domain names involved.
- Whether network monitoring is being conducted (filtering rules etc...).
- A list of any remediation steps that have been taken.
- If any data is being preserved, what process is being used and where it is being stored ?
- Updates to network diagrams and configurations.

### Malware details :
For each malicious file related to the incident
- The date and time of detection.
- How the malware was detected.
- The list of systems where the malware was found.
- The name of the malicious file, and what directory was it present in.
- What the detection mechanism determined, such as the name and family of the malicious file.
- If the malware is active during the IR and if active network connections are present.
- Whether a copy of the malware is preserved, either manually or through a quarantine process.
- The status of any analysis. Has the malware been analyzed for network and host indicators of compromise.
- Whether the malware was submitted to third parties, either through automated processes or via direct action by an employee.

(Build an attack timeline with all those informations.)

# Discovering the Scope of the incident
## Examining Initial Data
Assemble previous facts/data/informations to provide a better context of the detection event. 
Logique des 5 W et du H :
- Who ? Who is the user.
- What ? What department do they work for. What was the website. What data was transferred.
- When ? What time of day did it happen.
- Where ? One department. How many post (location).
- Why ? Data value.
- How ? Any website, were the user behind their computers.

## Gathering and Reviewing Preliminary Evidence
In this step, you have to determine what sources of preliminary evidence may be able to help and then decide which sources you will actually use.
May consider the following evidence sources (called "independent evidence sources") :
- Artifacts the malware directly creates on the system, such as files or registry keys.
- Operating system artifacts such as Windows prefetch, that are indirect artifacts.
- Application artifacts, such as Internet browser history or software metering tools.
- Network artifacts, such as firewall logs that might record network connections.

## Determining a Course of Action
Renember, there is no best way to make a decision or ideal path to solve a case.
Scoping process :
- Will the action help answer an investigative question ?
- Will the action answer my questions quickly ?
- Am I following the evidence ?
- Am I putting too much effort into a single theory ?
- Am I using multiple independent sources of evidence ?
- Do I understand the level of effort ?
- Am I staying objective ?
- Am I tracking the earliest and most recent evidence of compromise ?
- Have I uncovered something that requires immediate remediation ?
