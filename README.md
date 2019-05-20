# References
tidbits and one liners

# Mona
```
# Pattern create 5000 bytes
!mona pc 5000									                

# Find offet of string dj0d
!mona po dj0d									                

# Find 
!mona findmsp									                

!mona jmp -r ESP

# Generate bad characters, minus \x00
!mona bytearray -b '\x00'						          

# Compare full list of characters with output from register
!mona compare -f bytearray.bin -a 01A4F9E0		

# List all loaded modules and information about them
!mona modules									                

# Look for 'jmp esp' in essfunc.dll module
!mona find -s "\xff\xe4" -m essfunc.dll	  		

# Unicode venetian aligment stub
!mona unicodealign   # if EIP points to the start address already

# Set Mona Working Directory
!mona config -set workingfolder c:\monalogs
```
