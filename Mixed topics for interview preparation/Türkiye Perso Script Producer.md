#### **Producer to Perso
1. If file extension ends with ".gpg", should decrypt first, the following steps or else continue to step 2.
	1. Open Ubuntu 22 for decryption. 
	2. If it Türkiye go to this path "cd turkey_project/script/". if not create relevant folder accordingly.
	3. The source file in windows copy it into ubuntu in relevant path using below command.
		1. "cp </mnt/windows path>" destination path.
		2. Now decrypt the copied file using below command.
		3. "gpg --decrypt --output <decrypt filename> <source filename>" after execute this 
		 command it will ask to enter the password, The password hint "developer mail".
		4. Then copy to windows to decrypted file using below command.
		5. "cp sourcefile(decrypted file) destinationfile (in windows path - /mnt/windows path )"
2.  if file has endswit '.jcsh', open jcshll in below path 
	1. "D:\Soft\Smart Card\Jcshell_tool"
3. 