# MDFS software version O.AA Release Notes
## New features

This release supports :

 - Partitioning of large hard discs into 35 Mbyte logical discs. 
 - Up to 4 hard discs or partitions (formerly 2). 
 - Retrieval of individual files from tape.
 - 2048 accounts (numbered 000 to 7FF). See separate notes.

## Important change 
It is important to *park* the heads of hard discs if the equipment is to be moved. Previous versions of the fileserver parked the heads whenever the release discs button was pressed. Some modem disc drives will shut down completely when instructed to park the head, which is undesirable when simply changing *floppy* discs.

The new software will only park the heads if the release discs button is *pressed and held for five seconds* when the fileserver is running. This will cause the discs free lamp to illuminate steadily, indicating that the fileserver is completely shut down. When changing discs, the button should just be pressed momentarily, which will give the usual flashing discs free/online lamps.

Alternatively, the heads may be parked with the **Z** command in utility mode.

You are warned that transporting hard disc drives without having parked the heads can cause **permanent damage** to the surface of the disc. 

## Partitioning of large discs 
. Hard discs with a capacity greater than 35 Mbytes are now divided into partitions, each of which functions as if it were a separate disc drive. Each partition has a capacity of 35 Mbytes, except the last partition on each disc which will use up any remaining space on the disc. For example, a 95 Mbyte disc will have two partitions of 35 Mbytes plus one partition of 25 Mbytes. The fileserver can only support a total of 4 partitions when online. If discs with a total of more than 4 partitions are connected, the fileserver will use the fIrst partibm on each disc, plus the largest partitions available from the other discs up to the maximum of 4. Hence with a 95 Mbyte disc (35+35+25 partitions) plus a 37 Mbyte disc (35+2) the 2 Mbyte partition will be ignored. Four floppy discs can always be supported in addition to any hard discs.

When the fileserver is online, the separate partitions function as independent discs and are referenced by name. Use \*FREE to list the available discs/partitions.

In utility mode, the discs are referred to by letter (corresponding to the hardware controller number & drive number). If a large disc is selected, the system will prompt for a partition number (key I for the first partition, 2 for the second, up to the number of partitions on that particular disc). In the case of the Verify command, individual partitions can be verified or the whole disc can be verified at once by specifying a partition number of zero. Use the L (list discs) command to see the partitions available on all discs.

When using a tape drive, each tape can hold the contents of one disc partition. It is therefore useful to arrange your files on the disc such that frequently updated files are in one partition which can be backed up cfaily, leaving constant material (such as software packages, archive material, read-only databases etc.) on another partition to be backed up less frequently.


## Initialising existing hard discs
Customers with discs larger than 35 Mbyte which have been used with earlier versions of the fileserver will only have been able to use the first partition on the disc. When the new software is installed, the other partitions will still not be available as the root directories will not have been created when the disc was formatted - messages such as *Block 0 corrupt on drive E2* will be produced on the printer.

To create these directories, either the disc must be formatted again, or the roots of each partition must be initialised.  The format command now prompts for separate disc names for each partition. Beware that formatting a disc *erases all data from all partitions on that disc*. Only format a disc if you are happy to lose the data stored on that disc.

To initialise a partition without corrupting other data on that disc, the **I** (initialise disc) command may be used (in utility mode). Note that this command does not appear on the menu which is displayed, but works just like the commands that do appear on the menu. Before using the **I** command, type **L** to obtain a list of the discs and partitions available. Partitions which need initialising will say *Not afileserver disc* in place of the disc name - on discs formatted with the old software, partition 1 will contain the existing data, while partitions 2, 3 etc will need initialising. Now type **I** and enter the drive letter followed by the partition number. The current name of the disc will be displayed (this should say Not afileserver disc if the partition needs initialising), and the program will ask for a name for that partition.  Enter a name which is different from any other discs or partitions in your system. Finally you will be asked to type Y or N to confirm that the details are correct - type **Y** if you are sure that you have specified the correct partition. Take care **not** to initialise partition 1 as that would erase the data previously stored on the disc. Repeat the **I** command if there are more partitions to initialise.



## Retrieval of individual files from tape
It is now possible to read backup tapes without restoring the whole tape onto a disc. This is particularly useful for recovering files which have accidentally been deleted.

The facility works while the fileserver is online, by making the tape appear as if it were a very slow disc drive. It is not possible to write to the tape in this mode.

If a tape is inserted in the tape drive while the fileserver is online, a special directory **%TAPE** becomes available.  This is equivalent to the root ($) directory on the disc that was backed up onto the tape. Hence the following might be used to recover a BASIC program:

```
>*I AM FRED
>*DIR %TAPE
>*DIR FORM3
>*DIR FRED
>*CAT
FRED      (073)     Owner
ARGl                Option 00 (Off)  
Dir. FRED           Lib. LIBRARY

Besefix    WR/r     BFASTCOMP  WR/r     Bincode   WR/r     BMINITERM  WR/r
Bsafeterm  WR/r     Bxmit      WR/r     CARDS     D       cst         D/

>LOAD"Bxmit"
>*DIR
>SAVE"OldXmit"
>*UNLOADTAPE
>
```

No privilege is required to access the tape; the files on tape still have account numbers and access letters attached, so access is controlled in just the same way as files on the main disc. All the usual commands (eg. \*CAT, \*EX, \*INFO) can be used to inspect the contents of the tape. The utilities *Copier* and *Multicopy* can be used to copy groups of files.

One problem with this system is the slow response of the tape drive, which can cause *No Reply* errors. If such an error occurs, wait for the tape to finish winding and repeat the sequence of commands. The  necessary data should now be held in memory in the fileserver and so the commands will succeed immediately. The following guidelines will minimise the possibility of these errors:

 - Choose a time when there are as few people as possible using the fileserver, as other users will use up valuable memory space. 
 - Note that the example above selected the directory in a series of steps, rather than ***DIR %TAPE.FORM3.FRED** which would have required the fileserver to do all the work in the time allowed for one operation.
 - Always divide up long pathnames in this way. Use *Copier* or *Multicopy* on a BBC Master (or ET or Compact). This combination allows longer for each operation.

Before removing the tape, it should be *unloaded* to protect the surface of the tape from contamination. To do this, either press the Release Discs button, or use the ***UNLOADTAPE** command. When the tape has finished winding, it may be removed by pressing the large button under the tape slot. 

FS 0.AA release note
1987-09-20
**SJ**research 

