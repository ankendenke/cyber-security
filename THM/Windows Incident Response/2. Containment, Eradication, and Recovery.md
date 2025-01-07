Now that we have analyzed the malware and understood the infection vector, we can start the next step of the incident response process and proceed to contain the impact, eradicate the threat and recover the victim machine.

_**NOTE:** remember that, as incident responders, we also need to compile a report containing all the details of the actions we've taken. Before deleting any artefact from the machine or killing any involved process, remember to keep track of filenames, folders and other details that you've encountered: these are all very important data that need to be included in our report—and that may be requested to answer the questions at the end of this task._

## Containment

This step has already been partially addressed when our team carried out pre-response actions such as detaching the machine from the organisational network. This has hopefully prevented the malware from spreading further into the organisation's infrastructure.

What we can do now on the machine is kill the process to stop it from further “stealing” its resources. In the Task Manager, we can `right-click on the process > select End task`.

As responders, we must never fall into the mistake of becoming so focused on the incident at hand that we forget the big picture. This phase is meant for us to contain the threat, not only on the single compromised machine that we are aware of, but also across the whole organisation.

Now is the moment to compile a list of the IoCs collected during our analysis and action on them by sweeping the organisation with all the tools at our disposal (SIEM, EDR, network devices, etc.) for any occurrence of IoCs. In our scenario, we have the following collected IoCs that should be actioned on:

- The IP and port of the C2 server (as already mentioned in the previous task).
- The URL from which the macro-enabled Word document was downloaded.
- The URL embedded in the macro from which the malware was downloaded.
- The hash of the malware’s executable.

Searching across the network for these IoCs will help us identify and remediate any other compromised host within the organisation. Feeding the IoCs to monitoring tools—for example, adding the hash to an EDR blocklist or creating a SIEM rule to detect connection attempts to the URLs or the C2 IP—will prevent later infection from the same threat.

## Eradication and Recovery

To fully eradicate the threat from the machine, we will need to delete any artefacts that were dropped on it.

We can start by deleting the malware from the temporary folder where it was running. We must then also delete the Word document containing the macro that automatically downloaded the malware from the download folder. Finally, we must clear the download history from the browser to prevent the user from inadvertently clicking on the downloading link again.

And, most importantly, we must ensure that no persistence mechanisms are still in place. Thus, we must restore the `Run` registry key to its original value. To do so, we can search for `regedit` in the Windows search bar and select the `Registry Editor` app. To view the compromised `Run` key, we can paste the full path of the key in the bar at the top of the editor: `Computer\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`.

![A Registry Editor window, showing the content of the 'Computer\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run' key. The key contains a list of sub-keys. The last sub-key is named 'MyApp', is of type 'REG_SZ' and contains the string 'C:\Users\IRUser\AppData\Local\Temp\3d33es454e.exe'.](https://tryhackme-images.s3.amazonaws.com/user-uploads/60b31886758169005262132d/room-content/60b31886758169005262132d-1717776991756)

We will see a list of all the applications and processes configured to run at logon automatically. To delete the persistence, we can select the value containing our miner and simply `right-click > select Delete`.

With these actions, assuming that the malware analysis of the executable didn't discover any other persistence mechanisms or artefacts dropped by the malware, the machine is restored to its clean state.