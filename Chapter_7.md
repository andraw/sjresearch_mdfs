# Chapter 7: Utility Mode

## 7.1 Introduction

Utility mode is used to initialise discs, take backups and change some system parameters. Communication with the MDFS in this mode uses the program ***FAST** which can run as a sideways ROM, or in RAM. With FAST running, the BBC microcomputer is acting as a terminal connected (via the Econet) to the MDFS.  The BBC microcomputer sends characters from its keyboard to the MDFS; characters sent from the MDFS are received and printed on the screen. The actual controlling software (i.e. the bit that decides what to do when a given key is pressed) runs in the MDFS and the program is part of the File Server program (see section 4.4). The BBC microcomputer is acting as a rather elaborate Input/Output device.

## 7.2 Entering Utility Mode on the MDFS
In general, a slowly flashing Disc Free light means that either the File Server program has not been found, or that the File Server is waiting for you to press the Release Discs button. A quickly flashing Disc Free light
means that the File Server is searching for the File Server program. A flashing Utility Mode light means that the Utility program has been successfully loaded and is waiting for a connection from ***FAST** or a serial terminal. A steady Utility Mode light means that connection has been established.

## 7.2.1 For users with a FAST ROM fitted in a BBC Microcomputer.
From power-off, turn the File Server on with the front panel key-switch in the System position, make sure there is a disc with the File Server program in it and press the Release Discs button.
If the File Server is already on line, turn the key to the System position, log-on as a System-privileged user and type ***FINISH**. If there is a disc containing the File Server program already in the system the Utility
Mode program will be loaded and the Utility Mode light will flash. With no such disc, the Discs Free light will eventually flash and you should insert such a disc, press the Release Discs Button, and wait for the
Utility Mode light to flash.

Now use the BBC Microcomputer, (which is preferably near to the MDFS unit to save walking,) and type ***FAST**. Wait for the prompt:
```
    Station number to attach to:
```
 
and then type in the station number of the File Server, which will be 254 unless you have explicitly changed it. (Changing the File Server station number is described below.)

### 7.2.2 For users with no FAST ROM.
The procedure is much the same as above except that the ***FAST** program has to be loaded from the MDFS.  As a system privileged user, turn the key to the System position and type ***FAST** on a BBC Microcomputer, and at the prompt
```
    Station number to attach to:
```
DO NOT enter the station number but instead type ***FINISH**. Wait until the Utility Mode light flashes and then enter the station number.

If the message Key locked or Insufficient privilege appears after typing ***FINISH**, type **SHIFT-f1**, which should produce the message **OS command: \***. If it doesn't, press BREAK. Either way, you will need to type ***FAST** again, rectify the cause of the error above and re-type ***FINISH**. Then type in the station number as per the above instructions.

The BBC Microcomputer is now acting as a terminal to the MDFS, and  the Main Menu will be displayed:
```
    MDFS Utility Program ver 1.03
    (ROM version 1.00)
    
    A - Alter configuration parameters
    B - Boot Fileserver
    C - Copy whole disc
    D - Add to Winchester defect list
    F - Format new disc
    L - List discs
    P - clear Password file
    R - Rename disc
    S - Set File Server station number
    T - Tape Menu
    V - Verify Disc
    Z - Park disc heads
    
    Or press the front panel button
    to start the fileserver.
    
    Command (H for help) ?
```

## 7.3 Using Utility Mode
### 7.3.1 General Notes
N.B The \<Escape> key may be pressed at any stage to abort an operation and return to the main menu.  Pressing \<Return> when asked for a parameter will generally leave the previous value unchanged. For an explanation of the drive lettering conventions see section 7.5.

### 7.3.2 A - Alter parameters
This option sets some stored parameters which are held in the Battery-backed RAM in the MDFS. They control the operation of the serial printer and the floppy disc drives. The program will display the following menu:
````
          ALTER PARAMETERS
          
    Any changes will take effect
    when the file server is next
    booted except for the step rate
    which will change immediately.

    Typing <RETURN> will leave the
    current setting unchanged.

    Serial (RS232) parameters:

    Baud rate
    8 - 19200 baud
    7 -  9600
    6 -  4800
    5 -  2400
    4 -  1200
    3 -   300
    2 -   150
    1 -    75
    Current setting: 7
    Option : (1 - 8)?
```
Key in a number between 1 and 8 to change the Baud rate to suit the serial printer connected to the MDFS.  The system will then ask for the number of data bits per character, whether parity and stop bits are required to be sent, and what sort of handshake mode is appropriate. The most common values are shown here, and are the ones selected when the station number is reset (as described in §7.4).

```
    Current setting: 8
    Number of data bits (5..8) ?

    Parity:
      0 - No parity
      1 - Odd parity
      2 - Even parity
    Current setting: Q
    Option (0..2) ?

    Stop bits:
      1 - 1.0 Stop Bits
      2 - 1.5 Stop Bits
      3 - 2.0 Stop Bits
    Current setting: 3
    Option (1..3) ?

    Handshake mode:
      0 - CTS/RTS
      1 - Xon/Xoff
      2 - None
    Current setting: 0
    Option (0 .. 2) ?
```
The final parameter set by this command is the step rate for the floppy discs. If the step rate is set too fast for a drive, the system will revert to the slowest speed. The options available are:
```
    Floppy disc drive parameters:
    
    Step rate:
      0 - 3ms
      1 - 6ms
      2 - 10ms
      3 - 12ms
      4 - 15ms
      5 - 20ms
      6 - 30 ms
    Current setting: 0
    Option (0 .. 6) ?
```

### 7.3.3 B - Boot File Server
This will boot the File Server from Utility Mode into normal operation (Le. On line). A File Server program (the file **$.FS**) will be needed on one of the MDFS discs. Pressing the RELEASE DISCS button in Utility
Mode will also attempt to boot the File Server.

### 7.3.4 C - Whole Disc Copy
This copies one disc (floppy or hard disc) entirely to another, including the entire directory structure, password file, disc name, Account balances and Printer information. It will also format the destination drive
first, if requested.

Example of a floppy disc backup:
```
               WHOLE DISC COPY
               
    This option makes an identical copy of
    a whole disc. Previous contents of
    the new disc are destroyed, including
    disc name, account information etc.
    The new disc need not have already
    been formatted.
    
    Source drive (A .. H) ? A
    Destination drive (A .. H) ? B
    Format destination disc (Y/N) ? No
    
    Put source disc in A & push space <space>
    Name = floppyl size = 8OOK
    
    Put destination disc in B & push space <space>
    Name = olddisc size = 8OOK

    Copy complete - Verifying ...
    Verify complete - No errors
```
If the destination disc is to be formatted, the name will not be given as it will probably not be defined, so you must be careful that you are fonnatting the right disc. Formatting a floppy disc will take about two minutes and so will copying a whole disc.

The File Server memory cannot hold the contents of a whole floppy disc; so if the source and destination drives are the same, the system will prompt for you to insert the discs alternately several times.

It is also possible to copy between two winchesters using this command. This takes about 20 minutes.

### 7.3.5 D - Add defect list
This command is used to tell the winchester controller about bad sectors on a winchester. It is not supported by all makes of controller (notably the ACB 4000A and ACB 4070), but is supported by the R0752 drive.

If you have any bad sectors (and no drive is guaranteed wholly error-free) you will have probably noticed them from messages printed out while the File Server was On line. You should record the error number and block number of all such errors (so that you can see if the block is the same etc.). As soon as you have discovered that you have errors, you should verify the disc probably two or three times. Some errors are termed *soft*; these are sectors that can sometimes be read and sometimes not. Sometimes there is a power glitch which means that a sector could have been written badly (as opposed to the disc surface having a flaw on it). N.B. The block number printed by the File Server will be a logical block number, this will not be the sane as the physical number printed by the verify command. It is the physical block that must be entered into the Add Defect command. Entering a number that does not actually have an error in it will cause the message ```Sector read OK 5 times - are you sure?``` Discs with more than about six
errors should be regarded as suspicious and may require re-formatting.

#### 7.3.6 F - Format New Disc
This option will format floppy discs or hard discs and then write the necessary header information onto the disc. Any previous data on the disc will be destroyed. There is no need to format floppy discs before using the C (copy) option, as this option can format discs for itself.

For example:
```
               FORMAT NEW DISC
               
    Format disc in which drive (A .. H) ? B
    Disc name (max 10 chars) ? green<return>
    Push space to format disc in drive B<space>
    Formatting...
    Format complete
    Writing new root
    Verifying...
    Verify finished -
     All sectors OK
     
    Format another disc (Y/N) ?
```
Now an example of formatting a hard disc with an ADAPTEC ACB 4000A controller, such as are fitted to most BBC-compatible Winchester disc drives. Please note that option 'B' should be tried first, even if your
drive did not come from Acorn. This option assumes that the disc has already been fonnatted (but probably for another machine).

N.B. New defects can only be entered at format-time, due to limitations in the Adaptec controller (with a Rodime R0752, as supplied by SJ Research, defects can be entered at any time without having to re-format the disc).
```
    Format disc in which drive (A .. H)? E
    
    That is a Winchester disc
     - are you sure (Y/N)? Yes
  
    What sort of drive is it:
      A - SJ (Rodime R0752)
      B Acorn (Adaptec 4000A)
      D 20Mb Half height NEC/Mitsu
      E 40Mb Half height NEC/Mitsu
      F 20Mb Full height NEC/Mitsu
      Z - User defined drive
      
    Enter option: B
    Enter defect list (Y/N)? Yes
    Defects must be entered in ASCENDING
    order (maximum 16)
    All numbers should be in decimal.
    Cylinder: 4
    Head: 2
    Bytes from Index: 1002
    Another defect (Y/N)? No
    Disc name (max 10 chars) ? HARD-O<return>
    Push space to format disc in drive E
    Formatting ...
    Format complete
    Disc size = 31200k
```
N.B. The disc size printed may not correspond exactly to the notional drive size. This is due to several factors. Firstly the MDFS uses a sector size of 512 bytes which increases the storage capacity of the drive.
Secondly it rounds the disc size down to the nearest multiple of 5200k, and thirdly there is a maximum partition size of 36400k (until multiple partitions are supported this is the maximum size of the usable part
of anyone drive: multiple partitions can be added at a later stage). This 36400k limit is due to the amount of data that you can store on a tape drive.
```
    Verifying ...
    Verify finished -
     All sectors OK
```

### 7.3.7 L - List Discs
Tries to read all the discs (A .. H), and prints information on any that are connected to the File Server. It takes about a second to test for each disc, so do not be suprised if nothing happens immediately. For example:
```
             LIST DISCS
             
    Discs currently available:
    
    A: Name: Floppy1    size: 800K
    B: Name: green      size: 800K
    E: Name: Main       size: 800K
```

### 7.3.8 P - Clear Password File
This option is required if the password file has been corrupted on a disc, for example by saving rubbish over it, or if there exists no disc with a system user on it. (In general it is possible to work on the password file on any disc, by inserting another disc which has in its password file a system privileged user, with access to account 0)

The prompt will be:
```
           CLEAR PASSWORD FILE
           
    This option will remove a corrupt or
    unwanted password file from a disc.
    The disc will be left with
    NO PASSWORD FILE AT ALL : for security
    a new password file should be written
    (using EDITPASS) as soon as possible.
    
    Clear disc in which drive (A .. D) ? A
    Insert disc & push space when ready
    Name = floppy1 size = 800K
    
    OK (Y/N) ? Yes
```

If a disc without a password file is installed into the system, **anyone attempting to log on will have system privilege**. For this reason, it is advisable to use EDITPASS as soon as possible, to create at least a
null password file on the disc.

The F (format new disc) option creates a null password file automatically.

### 7.3.9 R - Rename disc.

All File Server format discs have a name associated with them. The name is up to 10 characters long and is subject to the usual rules governing filenames. When the MDFS is On line the only way for a client to select a particular disc is by its name, so it is wise to give each disc a unique name. In particular, the C option copies the name from the source disc, so the destination disc should be renamed if it is to be used for reading data off.

The process is:

```
                   RENAME DISC
                   
    Rename disc in which drive (A .. F) ? F
    Name = blue2   size = 20800K
    New name (max 10 chars) ? hardl <return>
    OK (Y/N) ? Yes
```

### 7.3.10 S - Set Station Number
This changes the station number of the MDFS. This number is stored in a special memory that is maintained by an internal rechargeable battery. No maintenance is necessary, but if the MDFS has been out of use for
more than about 6 months, the battery may have run down. In this case, follow the instructions in §7.4 to reset the station number to 254, then change the number (if required) with this option.

Any change in station number will be implemented when the File Server is next booted. The prompt will be:
```
Current station number is : 254
New station number        : 253 <return>
```

### 7.3.11 T - Tape Menu
This allows tape backups, etc to be made. For information about this menu see Chapter 8.

### 7.3.12 V - Verify Disc.
This reads all sectors of the specified disc. It tells you about any sectors which are unreadable or which are imperfect but readable (these are referred to as 'dodgy'). If a disc has any bad sectors on it you should try
verifying the same disc in a different drive. We suggest that you cease using that disc and transfer all data to another disc, preferably using **MULTICOPY**. The same applies to a disc with dodgy sectors if the data on that disc is valuable.

### 7.3.13 Z - Park disc heads
Winchester disc heads never actually touch the disc itself while in operation, but on most drives they do rest on the disc when the unit is switched off. It is usual therefore, to move the heads to an area of the disc which is not used for data storage before the power is removed, and especialy before transit. Some (older) drives even have a screw to secure the heads: refer to your drive manual for information. The Z command moves the heads to the innermost track of the disc (and beyond sometimes). This has the same effect as pressing the RELEASE DISCS button while the File Server is on line. N.B. Adaptec controllers take a long time (upto 10 Seconds) to reload the heads when the drive is next accessed. Any such access will automatically unpark the heads.

## 7.4 Re-setting the Station Number to 254
If the RELEASE DISCS button is held pressed while the power is turned on then the File Server station number will be set to 254 (the normal default). This will normally be necessary only in two circumstances:
The unusual circumstance of the File Server number having been forgotten (although it could often be found by running *STATIONS from another File Server).

The rechargeable battery that maintains the memory storing the station number has failed, usually because the MDFS has not been powered for more than about 6 months, this will cause a flashing system failure led.
In this case, leave the unit switched on for about 10 minutes, switch off, and then switch on again with the button held pressed. Note that the parameters set by the A option in Utility Mode are kept in the same
memory device: these will have been reset to their default values if the battery had failed. They can be changed back using the A option above.

## 7.5 Drive Letter Allocation
This section describes how the drives are labelled on the MDFS.

### 7.5.1 Physical Drives, Logical Discs and Partitions.
A complete physical drive is denoted by a single capital letter. Floppy discs are labelled A,B,C and D (as printed on the back of the MDFS), and winchester discs as E,F,G,H,I,J,K and L.

Some such winchesters may be too big for some parts of the system to cope with, and so are *partitioned* into smaller chunks. A partition of a drive is refered to by a letter followed by a number, thus **E2** refers to the second partion on physical drive E. The base partition is 1, thus there is no 0th partition. 

Logical disc numbers refer to a partition (but this may be the entire disc), and are only used when the File Server is On line. Such numbers are printed by ***FREE**. However to select a disc using ***SDISC**, you can only use disc names (although it would be possible to write a program to select a disc by number).

The logical disc numbers are allocated by the MDFS every time the File Server is started up or the button is pushed. The MDFS checks for the presence of drives E through L, and then checks all partitions of such
drives for valid disc headers (and will print the message Block 0 corrupt if the SJ Research header is missing), allocating a successive numbers to each non-corrupt partition. It then does the same for the floppy drives A through D. N.B. This means that if you have a floppy disc in drive A and a winchester connected as drive E, logical drive 00 refers to drive E and logical drive 01 refers to drive A, and not the other (more obvious) way round.

Disc Error messages contain either logical disc numbers or physical drive letters. The former is intended to be phased out as soon as possible, but was still extant in File Server code version 0.A3.

### 7.5.2 Winchester Disc Lettering
Winchester discs are connected to the SCSI bus connector. The SCSI bus talks to the disc controller, there being a maximum of 8 controllers (numbered 0 through 7) on any SCSI bus. Controllers 0, I ,2 and 3 are
allocated for disc drives, Controller 4 is for the Tape Drive, Controllers 5 and 6 are spare and Controller 7 is the MDFS itself. Some winchester disc drives have integral controllers (such as the SJ Research drive), the
rest (like the Adaptec ACB 4000A controller as used by BBC-compatible winchesters) have a separate controller and drive. The Adaptec will also support two drives per controller.  

**Table of Drive Letter Assignments:**
```
                                      (Drive 1 not supported
                                      by R0752 drives)
E    Controller 0, Drive 0       G    Controller 0, Drive 1
F    Controller 1, Drive 0       H    Controller 1, Drive 1
I    Controller 2, Drive 0       K    Controller 2, Drive 1
J    Controller 3, Drive 0       L    Controller 3, Drive 1
```
Thus if you have 2 SJ (R0752) winchesters you will have drives E and F, whereas with one Adaptec controller and two drives you will have drives E and G. See Appendix C for details on how to select controller numbers and drive numbers. 

Issue 16 Apr 1987
**SJ**research
