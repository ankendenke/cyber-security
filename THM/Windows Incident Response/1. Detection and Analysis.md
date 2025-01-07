## Scenario

In our scenario, we are acting as members of our Incident Response Team. A member of the organisation's SOC Team has called us to investigate and remedy a potential incident impacting a Windows workstation.

This is how the SOC Team has engaged us:

The user contacted the IT Team, reporting that his laptop started acting up and became extremely slow, to the point that he was having trouble working. The user couldn't pinpoint exactly what he was doing when the computer suddenly slowed down. He was browsing the web and working on some documents, as usual. He tried rebooting the machine, but performance was still very low.

IT has checked the machine's resources and found that the CPU usage is unusually high, even after closing all running apps. Suspecting a potential incident, IT has escalated the ticket to the SOC Team.

The SOC Team has verified that no alert was raised on the SIEM or EDR platforms for the workstation. The only anomaly that we have identified is some outbound connections on the perimeter firewall originating from the workstation's IP. The connections occur every second, and all have the same destination IP. The connections are not blocked by the FW. We have gone back to the user, who doesn't acknowledge these connection attempts.

Escalating to the IR Team.

For the scope of this room, we're assuming that all the pre-response steps have been correctly employed and that proper backups have been created before starting our investigation in order to preserve any evidence. We're also assuming that we're working in a safe environment, detached from our organisational network, to prevent the spreading of malicious artefacts within the organisation.

## Detection

The detection sub-step is deeply dependent on the previous preparation step: organisations need to put in place monitoring and detection systems such as SIEM (Security Information and Event Management), IDS (Intrusion Detection Systems), and EDR (Endpoint Detection and Response) solutions to help them proactively identify any potential threat within their infrastructure.

All these tools and systems must be integrated with policies and procedures to ensure that the proper teams are alerted in the event of a potential incident by occurrences of anomalies within the organisation's network traffic, suspicious access to systems or applications, or employees reporting suspicious activities or events.

In our scenario, the latest has happened: a user has reported a system anomaly to the IT Team. The IT Team recognised that the anomaly could be caused by a potential cyber threat and immediately escalated the incident to the proper teams.

## Analysis

The analysis sub-step is when the IRT actually comes into action. Keeping in mind the two goals highlighted in the previous task, we start our analysis by connecting to the machine and looking for the cause of the reported anomaly.

**Identifying the Threat**

As soon as we connect to the machine, we can easily verify what the user and IT Team have reported: the machine is very slow, and we can tell that something is using up its processing resources.

_**NOTE:** please note that the artefacts that you'll find in the attached VM—e.g. file names, PIDs, usernames, etc.—are different from those shown in the images below._

Let's open the Windows Task Manager and look at the `Processes` tab. There are many ways to open the Task Manager, the most straightforward being to `right-click on the Windows toolbar > select Task Manager from the menu`.

Windows Task Manager is a very useful system utility that provides information about running applications, processes, and system performance. It allows users to monitor and manage system resources and troubleshoot issues.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f9c7574e201fe31dad228fc/room-content/5f9c7574e201fe31dad228fc-1732004746044.png)  

We can see that no apps are currently running other than the task manager itself, although the system is still very slow. There must be some background task that uses up all the resources. To look at the background processes, we can click on `More details`. The view that opens is much more complete, and we can immediately see that the CPU usage is unusually high - as announced by the low machine performance.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f9c7574e201fe31dad228fc/room-content/5f9c7574e201fe31dad228fc-1732005418555.png)  

From this view, we can already identify the first anomaly: it looks like most of the processing power is being used up by a single background process. As seasoned incident responders, we are already alarmed by the uncommon name of the process, and we can easily hypothesise that this could be malware. We could even go on a leap and guess that it could be a crypto miner, considering what we know for sure: that it is using up the machine resources to carry out unknown actions.

To confirm our suspicion, we go on with our analysis and start by looking at the suspicious process properties: `right-click on the process > select Properties`.

![A window labelled Properties shows general information about the process with the name '3d33es454e'. The type of the file is 'Application (.exe)' and its location is 'C:\Users\IRUser\AppData\Local\Temp'.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324602517.png)

In the `General` tab, we can see another indicator of suspicion: the executable file's location is a temporary folder! This is very common for malware and extremely uncommon for legitimate software. Our hypothesis now seems even more concrete.

Remembering what our fellow colleagues from the SOC team have reported, an additional check we can perform to confirm our suspicion is verifying if the process is making any outbound connections. To do so, we will need the suspicious process's PID (process ID). We can find it by `right-clicking on the process > selecting Go to details`. This will open the `Details` tab and highlight the table row containing our process details.

![The Windows Task Manager displaying the 'Details' tab shows PID, Status, User name and other information about various running processes. The highlighted process with the name '3d33es454e.exe' has the PID equal to 6872 and the User name equal to IRUser.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324602453.png)

Let's open a command prompt by searching for `cmd` in the Windows search bar and opening the `Command Prompt` app. We can use the following command paired with the PID that we got from the task manager's details: `netstat -aofn | find "{PID}"`.

Command Prompt

```shell-session
Microsoft Windows [Version 10.0.19044.3324]
(c) Microsoft Corporation. All rights reserved.

C:\Users\IRUser>netstat -aofn | find "6872"
  TCP    10.10.17.57:49793      1.2.3.4:23123          SYN_SENT        6872
```

As our colleagues from the SOC have preannounced, we found an outbound connection attempt towards a suspicious combination of IP and random destination port. This adds to our suspicions: this could be the malware's attempt at contacting the Command and Control (C2) server to deliver mining data (if it's a crypto miner) or to get further instructions.

This combination of IP and port is a useful indicator of compromise (IoC). With it, we can perform various actions. For example:

- Immediately block the IP with a rule on the organisation's front-end firewall to prevent communication with the C2.
- Search for the IP in the organisation's network traffic logs to hunt for other occurrences of the malware within the organisation's infrastructure.
- Feed the IoC to a monitoring rule on the SIEM to proactively detect any later infection from the same malware.

To fully understand this malicious process's actions, we will need to carry out more advanced actions (such as a thorough malware analysis), but this goes beyond the scope of this room. We will assume that our IRT has analysed the executable and has, in fact, identified it as a crypto miner.

**Identifying the Infection Vector**

Once the incident has been confirmed, the IRT must understand and document the initial access vector. Some of the most common vectors are exploiting known vulnerabilities in internet-facing systems (web servers, application servers, FTP servers, etc.), phishing and social engineering, credential stuffing and brute force attacks, drive-by downloads, and supply-chain attacks.

Understanding the initial access vector is crucial because it helps pinpoint the 'hole' in the system, allowing for targeted remediation efforts to patch it.

Statistically, a workstation is most commonly compromised by careless actions carried out by end-users: clicking on a link in a phishing email, downloading a malicious attachment, or visiting a compromised website are all common infection vectors that exploit the inherent vulnerability within every organisation - its very human employees.

With this knowledge, we can re-read what the IT Team reported about the user's actions:

[...]

The user couldn't pinpoint exactly what he was doing when the computer suddenly slowed down. He was browsing the web and working on some documents, as usual.

[...]

We can hypothesise a drive-by download or a malicious file inadvertently downloaded from a phishing link. Let's look at the download history to see if anything catches our responder's eye.

We can open a browser by searching for “browser” in the Windows search bar. We will see that only one browser is installed: the default Microsoft Edge. Let's open it and look at the browsing history. The fastest way to open Edge's download history is to go to this URL: `edge://downloads/all`.

![An Edge browser window with a Downloads tab open. The page displays a list of files. The first file is named 'invoice n. 37484567 (1).docm', downloaded from the URL 'http://172.234.25.65'.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324602445.png)

The latest downloaded file catches our eye because it's weirdly named, and it was downloaded from a suspicious-looking link: in fact, it's unusual for a legitimate link to point to an IP address instead of a domain name. Moreover, the file has a very suspicious extension: `DOCM` indicates that the file is a Macro-enabled Word Document, which means that it most likely contains macros. We seasoned responders know that this could indicate the file might contain malicious embedded code. This code was most probably automatically executed when the user opened the document the first time.

A **macro** is a set of instructions or a script that automates repetitive tasks by performing a sequence of actions or commands within software applications. Macros are often used to save time and improve efficiency by streamlining complex or frequently performed operations. However, malicious actors can also leverage them to carry out dangerous actions, such as automatically downloading malware.

Maybe it's the source of our malware? Let's open it.

_**NOTE**: When we click on the file, Microsoft Word will open–slowly: we're painfully reminded that most of our computing resources are sucked up by the malware–and prompt us for a product key. We can ignore the prompt by closing the window._

![A Microsoft Office window prompting for a product key.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1730832127111.png)

_This will open a second window that we can dismiss by clicking on the_ `Next` _button, then on `Don't send optional data` in the next window, and finally on `Done`._

![A Microsoft Word window open on a document with the name 'invoice n. 37484567 (1)'. The text in the body of the document reads: 'To download the requested invoice n. 37484567, go to https://tryhackme.com/my-invoices and insert the invoice number as prompted'.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324603178.png)

The document looks suspicious and contains a link to a non-existing website page in its body. Moreover, although we have already noticed that its extension might indicate the presence of macros, Microsoft Word doesn't alert us about it. This likely means that any existing macro is being - and has been - automatically executed without the need for user execution.

We can see a list of macros contained in the document by going to `View > Macros`. In the newly opened window we can see that there is, in fact, a macro inside this document. Let's select it and open it by clicking on the `Edit` button on the right.

![A window labelled 'Macros' showing a list of macros contained in all active templates and documents. Only a macro with name 'AutoOpen' is present in the list. On the right part of the windows, buttons for different actions are shown: 'Run', 'Step Into', 'Edit', 'Create', 'Delete' and 'Organizer'.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324602560.png)

## Analysing the Macro

The VBA (Visual Basic for Applications) Editor opens in a new window, and we can start analysing the instructions contained in the macro for signs of malicious code.

![A Microsoft Visual Basic for Applications (VBA) window showing some VBA code. Two lines of the code are highlited in a yellow box. Both lines contain the string '3d33es454e.exe'. The full VBA code is provided below.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324602830.png)

**Click here to show a transcription of the macro's VBA code.**

Even if we might not be familiar with the VBA coding language, the two lines of instructions highlighted in the screenshot above should catch our eye, as they both contain the name of the executable that we have identified as the miner sucking the machine's CPU resources.

We can analyse the macro instruction-by-instruction to understand exactly what it does. If we aren't familiar with the Visual Basic for Applications (VBA) language, we can do a Google search of the instructions. Remember that we don't need to completely understand the code or be a programmer: our goal is to pinpoint the actions taken by the attackers in order to mitigate the threat to the best of our abilities.

The first line defines a macro named `AutoOpen`. This macro, when embedded in a Microsoft Office document, will automatically run when the document is opened.

![Snippet from the previous VBA code, lines 1-7. The line starting with 'If' is highlihted by a yellow arrow.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324602838.png)

The three subsequent lines use `Dim` to declare three variables of type `String`; the same three variables are assigned values with the instructions following shortly after.

The line highlighted by the yellow arrow in the screenshot above contains more complicated elements, and the full explanation of the instruction goes beyond the scope of this room. But briefly, it checks if a process with the same name as our suspicious executable is already running; if the process is found, the macro stops executing. This prevents the macro from downloading and running the same executable file multiple times if it's already active.

With the next lines of code, the URL of the file to be downloaded is assigned to the variable `strURL`, while the variable `strFilePath` is assigned the full path for the downloaded file by combining the system's temporary directory path (obtained via `Environ("TEMP")`) with the filename of our miner.

![Snipped of a single line of the previous VBA code, line 8.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324602477.png)

The next instruction constructs a command string to be executed by the command prompt (`cmd`). The command uses `certutil` to download the file from `strURL` to `strFilePath`.

`certutil` is a command-line utility in Windows used for managing and manipulating certificates and certificate authority (CA) databases. It is part of the Windows Certificate Services and can perform various functions. This is a very interesting way of stealthily downloading a file because it leverages a legitimate, pre-installed Windows utility, trusted by default and often allowed through security measures. This method avoids the need for additional tools that might be detected by antivirus software. The command generates minimal noise, blending in with normal administrative operations, making it less likely to be flagged.

![Snippet from the previous VBA code. Lines 9-11.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324602500.png)

With the next set of instructions, the command is executed in a hidden window (`vbHide`), effectively downloading the file without showing the command prompt to the user; then, after 10 seconds (if you enjoyed this little journey into VBA, you can analyse the `Wait` function defined at the end of the macro to prove that the `Wait (10)` instruction does just that), the downloaded file is executed in a hidden window.

![Snippet from the previous VBA code. Lines 12-14.](https://tryhackme-images.s3.amazonaws.com/user-uploads/66b36e2379a5d0220fc6b99e/room-content/66b36e2379a5d0220fc6b99e-1724324602775.png)

Finally, the macro constructs and executes a different command to add a Windows Registry entry in `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`, which ensures that the downloaded file runs every time the user logs in, ensuring persistence by making the executable run at startup.

The Windows Registry is a hierarchical database that stores configuration settings and options for the Windows operating system and installed applications. The `Run` keys in the Windows Registry specify programs to be automatically executed when a user logs in. For this reason, they are often leveraged by malware to ensure persistence in the infected system even after rebooting. Understanding the Windows Registry goes beyond the scope of this room, but we highly recommend that aspiring incident responders become familiar with it.

Now, something that the IT Team reported starts to make sense:

[...]

He tried rebooting the machine, but performance was still very low.

[...]

Let us make a recap of what we’ve learnt from our analysis of the macro:

- The macro, named `AutoOpen`, executes automatically when the document is opened.
- It immediately checks if a process with a name that matches the malware is already running. In this case, it terminates.
- If there is no such process, the macro leverages `certutil` to download the malware from a specific URL, and saves it to a temporary directory.
- It then stealthily executes the malware from a hidden command prompt.
- In the same stealthy manner, the macro finally ensures persistence by adding the malware to the `Run` registry key. This will allow the malware to be executed every time the user logs into the system, even after reboot.

Now it’s your turn to put into practise what we discussed in this task by investigating the attached VM to answer the questions.