Room progress ( 92% )
Target Machine Information

Title

THM-Internals

Target IP Address

10.10.205.218


Expires

36min 37s


Add 1 hour
Terminate
Task 1
Introduction









Task 2
Processes
























































Task 3
Threads















Task 4
Virtual Memory






















Task 5
Dynamic Link Libraries















Task 6
Portable Executable Format





































Task 7
Interacting with Windows Internals
Interacting with Windows internals may seem daunting, but it has been dramatically simplified. The most accessible and researched option to interact with Windows Internals is to interface through Windows API calls. The Windows API provides native functionality to interact with the Windows operating system. The API contains the Win32 API and, less commonly, the Win64 API.

We will only provide a brief overview of using a few specific API calls relevant to Windows internals in this room. Check out the Windows API room for more information about the Windows API.

Most Windows internals components require interacting with physical hardware and memory.

The Windows kernel will control all programs and processes and bridge all software and hardware interactions. This is especially important since many Windows internals require interaction with memory in some form.

An application by default normally cannot interact with the kernel or modify physical hardware and requires an interface. This problem is solved through the use of processor modes and access levels.

A Windows processor has a user and kernel mode. The processor will switch between these modes depending on access and requested mode.


The switch between user mode and kernel mode is often facilitated by system and API calls. In documentation, this point is sometimes referred to as the "Switching Point."

User mode	Kernel Mode
No direct hardware access
Direct hardware access
Creates a process in a private virtual address space
Ran in a single shared virtual address space
Access to "owned memory locations"
Access to entire physical memory

Applications started in user mode or "userland" will stay in that mode until a system call is made or interfaced through an API. When a system call is made, the application will switch modes. Pictured right is a flow chart describing this process.


When looking at how languages interact with the Win32 API, this process can become further warped; the application will go through the language runtime before going through the API. The most common example is C# executing through the CLR before interacting with the Win32 API and making system calls.



We will inject a message box into our local process to demonstrate a proof-of-concept to interact with memory.

The steps to write a message box to memory are outlined below,

Allocate local process memory for the message box.
Write/copy the message box to allocated memory.
Execute the message box from local process memory.

At step one, we can use OpenProcess to obtain the handle of the specified process.

HANDLE hProcess = OpenProcess(
	PROCESS_ALL_ACCESS, // Defines access rights
	FALSE, // Target handle will not be inhereted
	DWORD(atoi(argv[1])) // Local process supplied by command-line arguments 
);
At step two, we can use VirtualAllocEx to allocate a region of memory with the payload buffer.

remoteBuffer = VirtualAllocEx(
	hProcess, // Opened target process
	NULL, 
	sizeof payload, // Region size of memory allocation
	(MEM_RESERVE | MEM_COMMIT), // Reserves and commits pages
	PAGE_EXECUTE_READWRITE // Enables execution and read/write access to the commited pages
);
At step three, we can use WriteProcessMemory to write the payload to the allocated region of memory.

WriteProcessMemory(
	hProcess, // Opened target process
	remoteBuffer, // Allocated memory region
	payload, // Data to write
	sizeof payload, // byte size of data
	NULL
);
At step four, we can use CreateRemoteThread to execute our payload from memory.


remoteThread = CreateRemoteThread(
	hProcess, // Opened target process
	NULL, 
	0, // Default size of the stack
	(LPTHREAD_START_ROUTINE)remoteBuffer, // Pointer to the starting address of the thread
	NULL, 
	0, // Ran immediately after creation
	NULL
); 
