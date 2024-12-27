Wireshark is one of the most potent traffic analyzer tools available in the wild. There are multiple purposes for its use:  

- Detecting and troubleshooting network problems, such as network load failure points and congestion.
- Detecting security anomalies, such as rogue hosts, abnormal port usage, and suspicious traffic.
- Investigating and learning protocol details, such as response codes and payload data. 

Note: Wireshark is not an Intrusion Detection System (IDS). It only allows analysts to discover and investigate the packets in depth. It also doesn't modify packets; it reads them. Hence, detecting any anomaly or network problem highly relies on the analyst's knowledge and investigation skills.

**GUI and Data**  

Wireshark GUI opens with a single all-in-one page, which helps users investigate the traffic in multiple ways. At first glance, five sections stand out.

|   |   |
|---|---|
|**Toolbar**|The main toolbar contains multiple menus and shortcuts for packet sniffing and processing, including filtering, sorting, summarising, exporting and merging.|
|**Display Filter Bar**|The main query and filtering section.|
|**Recent Files**|List of the recently investigated files. You can recall listed files with a double-click.|
|**Capture Filter and Interfaces**|Capture filters and available sniffing points (network interfaces).  The network interface is the connection point between a computer and a network. The software connection (e.g., lo, eth0 and ens33) enables networking hardware.|
|**Status Bar**|Tool status, profile and numeric packet information.|

  
The below picture shows Wireshark's main window. The sections explained in the table are highlighted. Now open the Wireshark and go through the walkthrough.

![Wireshark - GUI](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/0a96b128d88d49f28e4b537b63bcfd3b.png)  

  
**Loading PCAP Files**  

The above picture shows Wireshark's empty interface. The only available information is the recently processed  "http1.cap" file. Let's load that file and see Wireshark's detailed packet presentation. Note that you can also use the **"File"** menu, dragging and dropping the file, or double-clicking on the file to load a pcap.  

![Wireshark - load pcaps](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/409e59f9a93d6a027b0041b968aae7a4.png)  

Now, we can see the processed filename, detailed number of packets and packet details. Packet details are shown in three different panes, which allow us to discover them in different formats. 

|   |   |
|---|---|
|Packet List Pane|Summary of each packet (source and destination addresses, protocol, and packet info). You can click on the list to choose a packet for further investigation. Once you select a packet, the details will appear in the other panels.|
|Packet Details Pane|Detailed protocol breakdown of the selected packet.|
|Packet Bytes Pane|Hex and decoded ASCII representation of the selected packet. It highlights the packet field depending on the clicked section in the details pane.|

  

Coloring Packets  

Along with quick packet information, Wireshark also colour packets in order of different conditions and the protocol to spot anomalies and protocols in captures quickly (this explains why almost everything is green in the given screenshots). This glance at packet information can help track down exactly what you're looking for during analysis. You can create custom colour rules to spot events of interest by using display filters, and we will cover them in the next room. Now let's focus on the defaults and understand how to view and use the represented data details.

  

Wireshark has two types of packet colouring methods: temporary rules that are only available during a program session and permanent rules that are saved under the preference file (profile) and available for the next program session. You can use the "right-click menu" or "View --> Coloring Rules" menu to create permanent colouring rules. The "Colourise Packet List" menu activates/deactivates the colouring rules. Temporary packet colouring is done with the "right-click menu" or "View --> Conversation Filter" menu, which is covered in TASK-5.

  

The default permanent colouring is shown below.

  

![Wireshark - packet colours](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/782c1d38f4502636cb2a8228e7675c9f.png)  

  

Traffic Sniffing  

You can use the blue **"shark button"** to start network sniffing (capturing traffic), the red button will stop the sniffing, and the green button will restart the sniffing process. The status bar will also provide the used sniffing interface and the number of collected packets.  

  

![Wireshark - traffic sniffing](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/a9ccd9cd2acd72480a4674ca576a4a51.png)  

  

Merge PCAP Files  

Wireshark can combine two pcap files into one single file. You can use the **"File --> Merge"** menu path to merge a pcap with the processed one. When you choose the second file, Wireshark will show the total number of packets in the selected file. Once you click "open", it will merge the existing pcap file with the chosen one and create a new pcap file. Note that you need to save the "merged" pcap file before working on it.  

**See image**

![Wireshark - merge pcaps](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/bbc3f7938f8d3086953d5b0342422019.png)  

View File Details  

Knowing the file details is helpful. Especially when working with multiple pcap files, sometimes you will need to know and recall the file details (File hash, capture time, capture file comments, interface and statistics) to identify the file, classify and prioritise it. You can view the details by following "**Statistics --> Capture File Properties"** or by clicking the **"pcap icon located on the left bottom"** of the window.

**See image**

![Wireshark - file details](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/1ccc88dc2b66e935f2f382387ce3c0ec.png)  

Answer the questions below

Use the "Exercise.pcapng" file to answer the questions.  

Read the **"capture file comments"**. What is the flag?  


[](https://github.com/boundary/wireshark/blob/master/doc/README.dissector)

![Wireshark - packet details](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/a09f80da3fd63b32e47842d93ead7db5.png)

![Wireshark - packet bytes](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/31f45c8e0e06d874d3826752839270df.png)  

  

![Wireshark - packet details](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/22a21052465fedc91fc4d1ec3beb6bd6.png)  

![Wireshark - layer 1](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/9d23e2081fa68e7d6f602aa8b0d316d9.png)  

  

![Wireshark - layer 2](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/cd06b372ae6338348ff521afb4c7243f.png)  

  

![Wireshark - layer 3](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d71eb4efc8d48a968a3e078045bd1511.png)  

  

![Wireshark - layer 4](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c373f8492470524a8f01fded43856a27.png)  

  

![Wireshark - protocol error](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/23bbe6ae6e8168cd0662998ff444b067.png)  

  

![Wireshark - layer 5](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/879aea2816018d27769fc8490e4af51b.png)  

  

![Wireshark - application data](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c2d9c3ce498c6f9044413b68df287c14.png)  

  

Task 4Packet Navigation

![Wireshark - packet numbers](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d52507e87088deb1597042d50900eef0.png)

  

![Wireshark - go to packet](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/cdb1e1d12c63fc831c7d94db634bbe0d.png)  

  

  

![Wireshark - find packets](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c8811df8ea0fa2b70fa90831d1ec9278.png)  

  

![Wireshark - mark packets](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/2c290f2f3c7b07223c86cd066751d19b.png)  

  

![Wireshark - packet comments](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/844bedc49bdd7dcaf26861a9cd2658fd.png)  

  

  

![Wireshark - export packets](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/86daa70b6cb8b93cb11535787222fb26.png)  

  

![Wireshark - export objects](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/16c22447c36bff2e415ea75a764854c8.png)  

  

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/53bb9769af677eede39a3ec9e1b368a3.png)  

![Wireshark - time display format](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d2333318ff4df99df252c6ee1c236619.png)  

  

  

|   |   |   |
|---|---|---|
||||
||||
||||
||||
||||

|   |   |   |   |
|---|---|---|---|
|||||
|||||
|||||

![Wireshark - expert info](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/31917b6f1e846d3383218cabf1c07caf.png)  

  

  
  

  

  

Task 5Packet Filtering

  

  
  

  

![Wireshark - apply as filter](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/463abd0a5cad55831b54a37c17092505.png)  

  

  

  

![Wireshark - conversation filter](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/6b31a8581e560286aee74fb9a608dfc9.png)  

  

![Wireshark - colourise conversation](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/b7a7ce6afa9c421e6bfaebac719d348c.png)  

  

  

![Wireshark - prepare as filter](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/0291e6095277eaebf8f9a8f8df0f1ec6.png)  

  
  

![Wireshark - apply as column](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/8eac68abb9c10fccce114f6ad803a5dd.png)  

  
  

![Wireshark - follow stream](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d578e89a1f4a526fb8ede6fdf1a5f1b5.png)

\
**Packet Numbers**

Wireshark calculates the number of investigated packets and assigns a unique number for each packet. This helps the analysis process for big captures and makes it easy to go back to a specific point of an event. 

![Wireshark - packet numbers](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d52507e87088deb1597042d50900eef0.png)

Go to Packet

Packet numbers do not only help to count the total number of packets or make it easier to find/investigate specific packets. This feature not only navigates between packets up and down; it also provides in-frame packet tracking and finds the next packet in the particular part of the conversation. You can use the **"Go"** menu and toolbar to view specific packets.  

![Wireshark - go to packet](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/cdb1e1d12c63fc831c7d94db634bbe0d.png)  

  

Find Packets

Apart from packet number, Wireshark can find packets by packet content. You can use the **"Edit --> Find Packet"** menu to make a search inside the packets for a particular event of interest. This helps analysts and administrators to find specific intrusion patterns or failure traces.

There are two crucial points in finding packets. The first is knowing the input type. This functionality accepts four types of inputs (Display filter, Hex, String and Regex). String and regex searches are the most commonly used search types. Searches are case insensitive, but you can set the case sensitivity in your search by clicking the radio button.

The second point is choosing the search field. You can conduct searches in the three panes (packet list, packet details, and packet bytes), and it is important to know the available information in each pane to find the event of interest. For example, if you try to find the information available in the packet details pane and conduct the search in the packet list pane, Wireshark won't find it even if it exists.  

![Wireshark - find packets](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c8811df8ea0fa2b70fa90831d1ec9278.png)  

  

Mark Packets

Marking packets is another helpful functionality for analysts. You can find/point to a specific packet for further investigation by marking it. It helps analysts point to an event of interest or export particular packets from the capture. You can use the "Edit" or the "right-click" menu to mark/unmark packets.

Marked packets will be shown in black regardless of the original colour representing the connection type. Note that marked packet information is renewed every file session, so marked packets will be lost after closing the capture file. 

![Wireshark - mark packets](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/2c290f2f3c7b07223c86cd066751d19b.png)  

  

Packet Comments

Similar to packet marking, commenting is another helpful feature for analysts. You can add comments for particular packets that will help the further investigation or remind and point out important/suspicious points for other layer analysts. Unlike packet marking, the comments can stay within the capture file until the operator removes them.

![Wireshark - packet comments](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/844bedc49bdd7dcaf26861a9cd2658fd.png)  

  

Export Packets

Capture files can contain thousands of packets in a single file. As mentioned earlier, Wireshark is not an IDS, so sometimes, it is necessary to separate specific packages from the file and dig deeper to resolve an incident. This functionality helps analysts share the only suspicious packages (decided scope). Thus redundant information is not included in the analysis process. You can use the **"File"** menu to export packets.  

![Wireshark - export packets](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/86daa70b6cb8b93cb11535787222fb26.png)  

  

Export Objects (Files)

Wireshark can extract files transferred through the wire. For a security analyst, it is vital to discover shared files and save them for further investigation. Exporting objects are available only for selected protocol's streams (DICOM, HTTP, IMF, SMB and TFTP).

![Wireshark - export objects](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/16c22447c36bff2e415ea75a764854c8.png)  

  

Time Display Format

Wireshark lists the packets as they are captured, so investigating the default flow is not always the best option. By default, Wireshark shows the time in "Seconds Since Beginning of Capture", the common usage is using the UTC Time Display Format for a better view. You can use the "View --> Time Display Format" menu to change the time display format.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/53bb9769af677eede39a3ec9e1b368a3.png)  

![Wireshark - time display format](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d2333318ff4df99df252c6ee1c236619.png)  

  

Expert Info  

Wireshark also detects specific states of protocols to help analysts easily spot possible anomalies and problems. Note that these are only suggestions, and there is always a chance of having false positives/negatives. Expert info can provide a group of categories in three different severities. Details are shown in the table below.

|   |   |   |
|---|---|---|
|**Severity**|**Colour**|**Info**|
|**Chat**|**Blue**|Information on usual workflow.|
|**Note**|**Cyan**|Notable events like application error codes.|
|**Warn**|**Yellow**|Warnings like unusual error codes or problem statements.|
|**Error**|**Red**|Problems like malformed packets.|

Frequently encountered information groups are listed in the table below. You can refer to Wireshark's official documentation for more information on the expert information entries.

|   |   |   |   |
|---|---|---|---|
|**Group**|**Info**|**Group**|**Info**|
|**Checksum**|Checksum errors.|**Deprecated**|Deprecated protocol usage.|
|**Comment**|Packet comment detection.|**Malformed**|Malformed packet detection.|

You can use the **"lower left bottom section"** in the status bar or **"Analyse --> Expert Information"** menu to view all available information entries via a dialogue box. It will show the packet number, summary, group protocol and total occurrence.

![Wireshark - expert info](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/31917b6f1e846d3383218cabf1c07caf.png)
![](https://downloads.intercomcdn.com/i/o/378475/452a29d68866e874f9ddccf0/9e0f012f15b6fc981dde2f1f5198d728.png)