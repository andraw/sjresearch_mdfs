# Chapter 6: Setting up printers

## 6.1 Overview
SJ Research File Servers all contain a *built-in printer* server with facility to connect one or more printers. One or two physical printers may be connected to the Modular Disc File Server: one to the parallel output and one to the serial output. The connection of printers is described fully in Appendix C.2.

Usually a *banner* will be printed before each user's output: this is some text set up by the system manager, which may also contain information (such as user identifier, time, date etc.) inserted by the Printer Server.

An example of a banner is:
```
SJ Research File Server *** Station 5 (FRED) 08feb85 15:21:04 ***
```

The banner file also specifies some text to be added at the end of each user's printout. An example may be a row of asterisks followed by a page throw.
Each *physical printer* may have up to four different banners available, and these are distinguished as different *logical printers*. Thus there may be up to eight logical printers on each SJ Research printer server.

***PSLIST** will list all the printer servers and logical printers available on the network. The system manager has to give names to the logical printers connected to the File Server, using the program **Editprint** (see 6.3.1 below).

Directing output from a BBC computer to the network printer is quite complicated. In a simple system, where there is only one Printer Server and only one printer, ***PS** will select it. In most cases, ***PS \<name>** will be required to select a particular printer by name.

For detailed control of printing, there are three settings to be adjusted : whether your computer uses a directly connected printer or a network printer, which printer server station is used, and which *logical printer* is selected within that station. The first two of these are remembered by your BBC micro, while the logical printer setting is remembered (separately) in each printer server. ***PS**, ***PRINT**, ***PRINTER** and ***FX5,4** can all be used to adjust different combinations of these settings.

When first switched on, a BBC micro will assume that a directly  connected parallel printer is to be used, and if the network printer is then selected it will use the printer server at station 235. The default logical printer can be adjusted by use of *Editprint* (see 6.3.1 below). Remember that if the equipment is left switched on, any changes will be remembered indefinitely, so it is not wise to rely on these default settings.

***PS** alone will choose (at random) any printer server station that has a working printer connected, but will not change the logical printer setting. ***PS \<name>** will select a printer server station with a printer of that name and select that logical printer in all printer servers that have one. ***PS \<number>** will select that printer server number regardless of whether it has any printers connected, and will have no effect on logical printer settings. Hence .PS is useful if there is only one possible printer for it to select, ***PS \<name>** is the most commonly used variant, and ***PS \<number>**  can be useful if there are several printers with the same name.  All varients of  PS also have the effect of ***FX 5 4** and possibly ***FX 6** - see below.

***PRINT** changes the selected printer server station number to that of your currently selected File Server.  The logical printer setting is not changed: if there is more than one logical printer available, ***PRINTER** can be used to select between them. ***PRINT** also has the effect of ***FX 5,4** and ***FX 6**.

***FX5,4** instructs the BBC computer to use the network rather than a directly connected printer. Neither the printer server station number, not the logical printer name are affected by *FX 5.

***PRINTER \<name>** adjusts the logical printer setting in the printer server attached to the currently selected fileserver only. It has no effect on any settings in the BBC computer. It is therefore useful in conjunction with ***PRINTOUT**, which can only use the current fileserver, or ***PRINT** which forces the BBC computer to use the current file server as printer server. ***PRINTER** alone will display the current setting without changing it.

In summary, ***PS** is the most useful command for general printing from a BBC computer, as it sets all three pieces of information. The other commands are available for fine control in very complex situations.

The ***PS** command actually loads a program called PS from the library directory. There are two versions supplied, called **PSFX6** and **PSnoFX6**. If your printer does an automatic line-feed after every carriage return, then use PSnoFX6, otherwise use PSFX6. The latter does the call ***FX6,O** which allows the BBC computer to send line-feed characters to the printer. When first supplied, the library has PSfx6 under the name PS, and PSnoFX6 under its own name. If your printers are set for auto line-feed, type:
```
   *DIR $.library
   *RENAME PS PSfx6
   *RENAME PSnoFX6 PS
```
to make the correct version available to your users. The utility ***CHECK** can be used to tell which version is currently named PS.
If you have two printers, one of each type, use PSnoFX6 as PS; and instruct users to type ***FX6,O** after ***PS** if they have selected the printer with automatic line-feeds. Alternatively, see if you can disable the
automatic line-feed on the printer, so that you can then use PSFX6 throughout.

### Special note for BBC Master Series computers
BBC Master Series computers (Master 128, Master ET, Master Compact etc.) have the ANFS ROM fitted.  This means that there is a version of ***PS** built in to the computer, and that the default settings which were fixed on the BBC computer can now be configured by the user.

The version of **PS** built in to the ANFS is broadly similar to the version supplied on the fileserver disc, but the messages it produces are different and it does not set ***FX5,4** or ***FX 6**. The easiest solution is to always type ***/PS** (rather than ***PS**): this will use the standard version from disc, regardless of whether it is typed on a standard BBC computer or a Master Series computer.

Alternatively, the built-in ***PS** can be used, and the values of ***FX 5** and ***FX 6** set up permanently in the CMOSRAM.

To set ***FX 5 4** as default:
```
   *CONFIGURE PRINT 4
```
To set ***FX 6 0** as default:
```
   *CONFIGURE IGNORE
```
Alternatively, to set ***FX 6 10** (equivalent to PSnoFX6):
```
   *CONFIGURE IGNORE 10
```
To set the default printer server station number:
```
   *CONFIGURE PS <ps number>
```
Remember that there is no protection against any user re-configuring these settings, so in situations where many people use the same computer it is easier to use ***/PS*** rather than relying on the configured settings.  Note also that newly supplied Master Series computers will probably have these settings configured inappropriately.

## 6.2 Everyday printer management

While it is hoped that users will send listings of programs and text from wordprocessors it is likely that, by accident, a user will select and start printing to the network printer when he does not intend to. If the printer
data is being spooled to disc then the user may not realise that he has a \<Ctrl B> active. This will lead to a print job being held in the **%PRINTQ** directory, taking space on the disc.

If the user is aware that he has accidently sent spurious text then a ***FLUSH** can be used to delete all print jobs whose username and station number match those of the user, whether those jobs are currently printing or not. For the printer managers (users who have access to the main account number of the **%PRINTQ** directory) there are additional commands to control the printers:
```
   *PS TOP [<printer name>]
```
This command suspends printing on the specified printer (or both printers if no name is supplied). Any jobs which are currently printing are not deleted, but the corresponding file in the **%PRINTQ** is closed, and may hence be manually deleted if necessary. If printing is restarted without changing anything, the same job will be re-printed from the beginning, which may be useful after a paper jam has been cleared.
```
   *PGO [<printer name>]
```
Restarts printing on the specified printer after is has been suspended by ***PSTOP**. Both printers are restarted if a name is not supplied. ***PGO** has no effect on printers that have not been suspended. Note that printing will also be restarted on both printers by the Save changes & exit option in **Editprint**, and when the fileserver is restarted. Hence if the printers are accidentally suspended, they may unexpectedly start printing the next time that the fileserver is restarted or the discs are changed.

**%PRINTQ** is a directory on the lowest numbered disc on the File Server. It can be accessed by name like any other directory but does not appear on the catalogue of the root directory.  **%PRINTQ** need not have a pathname given for it, even when it is accessed from another disc.

Each item waiting to be printed is transferred to **%PRINTQ** and given a unique name, starting from AAOO and going up to ZZ99. Then, when a printer becomes free, the directory is checked in alphabetical order for the first job waiting to use that printer. When each job has been completed, its entry is erased from the print queue and the next job is printed. Thus, by default, print jobs to a particular physical printer  are carried out in the order in which they are submitted.

The account number for each print job is reset to that of the **%PRINTQ** directory, so that users' own account credit is not used up. However the auxiliary account number of a print queue entry is set to the user's personal account number. This usually means that a user has owner access to his own print jobs, so he has read access to them and can also delete them from the print queue.

Information about entries in the print queue can be obtained with the usual directory commands ***CAT**, ***INFO** and ***EX**. Print queue entries have a special access code **/spl**, which indicates their status as print jobs. Entries submitted by ***PRINTOUT** (see Section 6.5) will have access code **/prt**. Like directories (which have **D/**), these access letters cannot be changed by the ***ACCESS** command, but it is possible to add **P** or **L**. Unlike ordinary files, the **L** access letter does not prevent the file from being deleted by the user, but it does prevent the system from printing the file.

The formats of ***EX** and ***INFO** are also changed for print jobs, so that the user and station number originating the print request is given in place of the load and execute addresses of a file, and the logical printer selected in place of the creation date. For example, **EX %PRINTQ** might give
```
%PRINTQ (126)   Public
Main-V          Option 03  (Exec)
Dir. Karen      Lib. Library
AA33 DIANA      at Stn.OOS 00008A /spl HOLD 13feb86 14.32 01 (FF)
AA34 TONY       at Stn.064 00DC43 /spl PARALL today 11.59 01 (FO)
```

There are three special logical printer names: **HOLD**, **AUTO** and **PRINT**. Jobs sent to the **HOLD** printer are not printed: they remain in the print queue until they are either deleted or rerouted to a real printer.

**AUTO** automatically selects whichever printer is free, in an order of preference set up by **Editpass**. Both **AUTO** and **HOLD** operate like any other logical printer: they can be specified in ***PS** or ***PRINTER** and jobs can be sent to them by ***REROUTE**. **PRINT**, however, is a special name for use in ***PS** which leaves the logical printer setting unchanged. **PRINT** will never appear on jobs in the print queue: they will be marked with the logical printer setting which was actually in force. 

Printer managers (who own the account number of the **%PRINTQ** directory) will have owner access to all entries, and will be able to read, rename and delete any of them. Because the queue is sorted into alphabetic order, changing the names of files in the print queue will  change their relative priorities. The printer manager can thus "queue-jump" important jobs to the head of the print queue by using ***RENAME** and some suitable name like !URGENT. (! has highest alphabetic priority, followed by the numbers I to 9 and then the main alphabet.) Naturally enough ownership of the print queue account should only be given to trustworthy people like the system manager.

When the File Server is re-started, the next name for a print queue entry is reset to AAOO. If it is important that entries from the stored print queue are printed first, they should be renamed to restore their original priority. This is most easily done with the command:
```
   *RENAME %PRINTQ.* %PRINTQ.l*
```
before any new entries are added to the print queue.

Privileged users can also create ordinary files and sub-directories in the print queue directory if they so wish.  While this will not affect the print queue operation, it is not recommended.

The printer manager will be able to selectively remove jobs by ***DELETE**. If the job is currently being printed then it is necessary to use ***PSTOP** otherwise the error **Already open by 2.000 \*-SPOOL-\*** will be returned.

In order to remove spool files that have been opened by users with \<Ctrl-B> who have then gone away or switched off their machines it is necessary to log them off before attempting to delete their output. The
easiest way of doing this is to find the station number of the offending spool file by use of ***INFO** or ***EX** and then log them off using ***LOGOFF \<station number>**; you will then be able to delete the entry. It is advisable to reroute such jobs to the **HOLD** printer before logging off the offending user, as the job might otherwise begin to print.

Note that ***LOGOFF** when used with a station number is a system privileged command, so you will have to be logged on as a system user to use it. Alternatively, ***LOGOFF** can be typed at the station in question, which does not require system privilege. (***LOGOFF** is more powerful than ***BYE**: ***BYE** does not fully log off a user if the file server thinks that they are still printing, until a ctrl-C is received).

## 6.3 Setting up the Printers
The File Server has to keep a number of pieces of information about the printers connected to it. The electrical parameters of the serial printer (baud rate etc.) are kept within the fileserver itself, but all the other information is kept on disc. Most of the settings are kept in a special part of the disc which can only be accessed by the **Editprint** program. If you are using more than one disc, this information will be kept on the
first disc in the system (i.e. the first in the list produced by ***FREE**). This will be a hard disc if you have one, but will otherwise be the floppy disc in drive A. If you use different floppy discs in this drive, remember
that you will need to use **Editprint** on each of them. The **Editprint**  information is copied by the copy discs option in utility mode.

Further information is kept in **banner files**, but these are ordinary files which require no special precautions.

### 6.3.1 Editprint
Editprint is a BASIC program, which can only be used by system privileged users.
To adjust the printer settings, type:
```
   CHAIN "EDITPRINT"
```
The program will respond with:
```
   Edit logical printer details
   Change system messages
   Set up initial choices
   Save changes and exit
```
Choose an option by moving the menu bar, with the cursor keys, over the option and pressing return.

#### Option 1 - Edit logical printer details
This will result in a list of logical printers being displayed on the screen, for example:
```
   1.Micro1         Parallel
   2.Serial         Serial
   3.Nobann         Parallel
   4.               Serial
   5.conden         Parallel
   6.Epson          Serial
   7.               Parallel
   8.               Serial
```
The right hand column indicates which *physical* printer will be used: while the File Server only has connections for two printers, it is possible to have several printer names associated with each one.

By moving the menu bar and pressing return, an individual logical printer can be selected, and its details will appear:
```
   Name: MICROL
   Printing enabled: Yes
   Bannerfile: Banners.Parallel
   Spool to Disc: Yes
   Anonymous Users allowed: Yes
   Account Ownership required: No
```
Again the menu bar highlights one item. Yes/No items can be changed by pressing **space**, while other items can be changed by typing a new value, followed by **return**. **Return** on its own writes any changes back to the File Server and returns to the main menu. Escape discards any changes which may have been made by mistake.

**Name** is the name which users will quote to specify that particular logical printer. Printer names may be up to six characters long. The names **PRINT**, **HOLD** and **AUTO** are reserved and must not be given to a printer. If the printer name is blank (i.e. consists of spaces), that printer is disabled completely.

**Printing enabled** controls whether output sent to this particular printer will be printed. It does not prevent users from generating output, which will be spooled to disc. Hence it is possible to have two logical printers named 'PAPER' and 'LABELS', only one of which is enabled at any time. Users can generate both types of output, and any documents sent to the disabled printer will be held until someone changes the stationary in the printer and uses EDITPRINT to enable the corresponding printer name. Another use for printer names with printing disabled is to allow users to generate output for a remote despooler program: this ensures that the File Server itself does not try to print jobs intended for a distant printer.

**Banner file** gives the name of a text file which controls the banner that is printed at the top of all printer output. The various possibilities for the contents of the banner file are described in section 6.3.2. The file
name is looked up starting from $ on the first disc drive, so **banners.fancy** would be equivalent to **$\*.banners.fancy**. If the file cannot be found, or if the name is blank, no banner is printed at all: this is useful for non-standard devices such as graph plotters. Note that the system must have read access to the banner file: the access string on the file would usually be set to **WR/**.

**Spool to Disc** controls whether printing starts as soon as some data arrives, or whether it is spooled onto disc and only printed when the whole document has arrived. In either case, data will be spooled to disc if the printer is already busy with another user's output. For fast printers, it is preferable to spool to disc, preventing one user from claiming the printer for an extended period. For slow printers, or graphics dumps,
it saves time to start printing immediately.

**Anonymous users allowed** control whether users who have selected this logical printer, but are not logged on to the File Server, may print. If this user presses \<CtRL B> then he will be logged on as **ANONPRINT** or the default user if ANONPRINT does not exist.  Having finished printing the user will be automatically logged off.

**Acount ownership required** controls whether a user requires a specific account number to select this logical printer, beware that if this printer is listed under initial choices then the account ownership check will be bypassed.

#### Option 2 - Change System Messages
This enables you to set the level of system messages. If you select option two from the editprint menu the following will appear on the screen:
```
   0 = serial
   1 = parallel

   System message Parallel
   Message Level is 0

   N.B. System error messages are ALWAYS sent to the printer.
```
By typing zero or one, the printer port used for system messages can be selected. It is not possible to disable system messages altogether, as the system has to have some way of displaying warnings of impending
failures.

The system message printer should be one which is usually connected, or if there is usually no printer connected, the type of printer which can most readily be found in emergency should be selected. Note that the screen of a BBC micro can be used as a serial terminal if a suitable lead is available.

If the menu bar is moved down, a list of the possible message levels appears. The selected level can be changed by typing a number followed by **return**.
```
0 = off
5 = logon/logoff
7 = errors
10 = maximum users & *commands
11 = load/save
15 = *cat and opens
128 = aborted loads
130 = Fn codes
150 = net errors
170 = map building
200 = disc read/write
250 = all sucessful net transactions
255 all activity to JPROC

System message parallel
message level is 0
```
These represent cummulative levels of system messages (7 includes the message of 5 and 0). Although the system message level may be set to 0, system messages after catastrophic errors will still appear on the printer. The printer specified can also be used for user's output, since the system messages will be separated by a page throw and header. If the message level is not 0 then any corresponding logical printers should be
set to *not enabled*. This will prevent users from printing to them. The usual message level is zero.

#### Option 3 - Set Up Initial Choices
This option allows you to specify the default printer for users who do not select a particular printer, and to indicate the first and second choices of printer when AUTO is selected as a printer.

The screen will display:
```
   Priority of Printer       No          Printer
                             0           STOP
   1st Micro1                1           MICROL
   2nd Epson                 2           SERIAL
                             3           Nobann
                             4
                             5           conden
                             6           Epson
                             7
                             8

   Default AUTO              9           Hold

   New default choice.
   Press 0-9 to select printers
```
Use the up and down cursor keys to select the piece of information you wish to change and enter the required printer number. The display on the right hand side of the screen lists the available printers. If the second choice is set to zero, then **AUTO** will be equivalent to the first choice printer. If the first choice is set to zero, the **AUTO** printer will be disabled completely.

Remember that any user can select and print to the **AUTO** printer, bypassing any restrictions that may be placed on the first or second choice printers. Hence it is not usually sensible to specify as first or second choice a printer which has account ownership required.

It is conventional to set up the **AUTO** printer such that the first choice is the fastest printer for long listings, with the second choice being the other printer with a similar banner. If the second printer is unsuitable for listings, the auto printer would usually specify just one choice, or be turned off altogether.

The default printer is the one which will be used if a user sends data for printing without selecting a particular printer. The File Server still checks whether the user is permitted to use that printer, so restricted access on the default printer will prevent some users from printing  without explicitly selecting a printer to which they do have access.

Popular settings for the default printer are 0 (AUTO) or 9 (HOLD).

#### Option 4 - Save Changes And Exit
This option puts into effect any changes which have been made through the other **Editprint** options. Note that the changes have already been written to disc, so leaving **Editprint** without using this option will not discard the changes: they will come into effect next time the fileserver is re-started.

### 6.3.2 The Banner File
The printer server usually prints a heading at the start and end of each piece of printed output, known as the *banner*. The name of the file to be used is set up with the Editprint program (see section 6.3.1). The format of the banner is controlled by a file associated with each printer name, and it may contain both fixed text and some information about that job, such as the name of the user that generated it and the date. It is possible to specify the same banner file for all the printers, but it is often useful to have more than one banner. In particular, it is possible to have two or more printer names which specify the same printer but with different banner files: a printer name **NLQ** might specify a banner file containing the necessary control codes to set that printer into near letter quality mode, while there would be another printer name **DRAFT** which used the same printer but left it in draft mode.

If no banner file has been specified, or the file specified is not found, or the system has not got read access to it (this means that the file must have letter *R* owner access), then the users' text will be printed without a banner or endtext: no error message will be produced.

The disc supplied with the fileserver has a directory **$.BANNERS**, containing (initially) two sample banner files, called SIMPLE and FANCY. The banner for each logical printer is initially set to no file, and the
system manager will have to select one of these two files, or create one of his own, in order to get printer banners at all.

It is possible to allow selected users to change the banner for their own purposes, by giving them access to the account of the banner file preferably having set this account to a unique value, so that the users in
question cannot change any other files). It is recommended that the user uses the ***RENAME** command, to change the name of the banner file to something else, and again to rename the desired file as the banner file: this avoids the chance of accidentally deleting the main banner file.   The users who are allowed to change the banner file will have to be responsible themselves for changing it back after they have finished.

The banner file is a simple text file, of the sort created by ***BUILD** or **Wordwise**. It contains a mixture of straightforward text, which is just printed out, and special symbols which are replaced by the information
they represent. The file split into two parts: the banner which is printed at the top of a user's output, and the endtext which is printed at the end, separated by the special symbol **\<BANNER>**.
```
   end-text<BANNER>banner text
```
The special symbol **\<BANNER>** must be enclosed in angle brackets as shown. Note that the end-text (the characters to be printed after the user's output) comes first, and the banner text itself after the word **\<BANNER>**. The texts will be printed literally until a special symbol is encountered.

The banner or end-text may contain special symbols from the list below. Note that all the symbols are enclosed in angle brackets <>. A carriage return character in the text will cause a carriage return on the printer; note that if your printer does not do an automatic line-feed after each carriage return, then a line feed character (or **|J**) should be put after each carriage return character (unless you intend to over-print lines).

There are three symbols that do not cause anything to be printed directly, but they select which of three possible times are printed when the identifiers \<HOURS>,\ <MINUTES> etc. are used.

Symbol | Description
-------|---------------
|\<NOW> | selects the current time of day, at the moment when printing is actually taking place. The time to be printed is frozen at the instant when the \<NOW> symbol is processed: this avoids inconsistent results if the clock ticks between the printing of the hours and minutes. If another \<NOW> is encountered (in the end-text, for example), this will freeze a different value, as time will have elapsed during the printing of the intervening text.|
\<START> | selects the time of day at which the printing job was initiated, from the user's computer. Note that, especially when print spoofing is used, this (and \<END> below) may be substantially earlier than the time given by \<NOW>.
\<END> | selects the time of day at which the user finished sending characters to the printer.

The following identifiers cause part or all of the time and date as selected above, to be entered into the banner or end-text string. The default time selection is **\<START>**.

Symbol | Description
-------|---------------
\<HOURS>| gives a two digit hour in the 24 hour clock, with leading zero printed. For example 6 pm will be printed as 18. 
\<H>|is a synonym for \<HOURS>.
\<MINUTES>| gives the minutes past the hour as two digits between 00 and 59, with leading zero printed.
\<M>|is a synonym for \<MINUTES>.
\<SECONDS>| gives the seconds past the minute as two digits between 00 and 59, with leading zero printed.
\<s>|is a synonym for \<SECONDS>.
\<12HOURS>| gives the hour in the 12 hour clock, with leading zero replaced by a space.
\<AM>| gives am or pm as appropriate. Note that noon is deemed to be pm.  The day of the month, as two digits, with leading zero replaced by a space.
\<DATE>| The day of the month, as two digits, with leading zero replaced by a space.
\<ST>| gives the correct suffix to the day of the month. For example, on the first of the month, the string inserted by \<S1'> will be st, on the second, nd, on the fourth th and so on.
\<MONTHNAME>| gives the full name of the month, e.g. January. No leading spaces are printed.
\<ME>| gives a three letter abbreviation of the name of the month, beginning with a lower case letter. January will be printed as jan.
\<MTH>| gives the number of the month as two digits with leading zero printed. January will be printed as 01, and December as 12.
\<MONTH>| will be printed as 01, and December as 12.
\<YEAR>| gives the last 2 digits of the year. 1987 will be printed as 87.

The remaining symbols allow the banner to print the users name and station number and deal with the layout of the banner.

Symbol | Description
-------|---------------
\<USERNAME> | gives the user identifier logged on at the station that originated the print job. No leading spaces are printed.
\<STATION> | gives the number of the station that originated the print job. The station number is printed with leading zeroes and with the network number (if the station was on a different network), but no leading spaces are printed. For example, station 2 on the local network will be printed as 002, but station 43 on network 7 is printed as 007.043.
\<BANNER> | The delimiter between the end-text (which should appear in the file first) and the banner proper. See description above for full details.
\<B>| is a synonym for \<BANNER>.
\<MARK>| gives a reference point for \<TAB> (see below).
\<TAB nnn>| pads out to a position nnn spaces from the last \<MARK> identifier. There must be one space (only) between the word TAB and the number. If no \<MARK> has been given, this command pads out to a position nnn spaces from the beginning of the text. Note that a carriage return does not reset the value of \<MARK>, and that only the least significant byte of nnn is read. <TAB 0> is illegal: the instruction will be ignored and the word \<TAB 0> will be printed. If the number after TAB is less than the current character position, then the tab will move to the position 256+nnn.

Note that all the special symbols are enclosed in angle brackets <>. Unrecognised special symbols will be printed literally.

Control characters may be sent to the printer either by direct inclusion in the banner file (if your editor allows this), or by use of the 'I' character:

I introduces a 'control' character, e.g. lA inserts <ctrl-A>.
I? inserts ASCII character &7F (delete).
I! inserts the next character with &80 added (Le. top bit set).
1< or I> inserts characters < or >.
11 prints the 'I' character itself.

#### 6.3.2.1 Table of standard characters
The following table shows, for each possible character code, a sequence of characters that can be inserted in a banner file to produce that code. In all cases except characters 60, 62 and 124, the same effect can be achieved by inserting the character values directly: the advantage of  using these sequences is that the resulting banner file can be inspected with ***TYPE** or a standard text editor.
```
0   |@         27  |[         54  6          81  Q          108 l
1   |A         28  |\         55  7          82  R          109 m
2   |B         29  |]         56  8          83  S          110 n
3   |C         30  |^         57  9          84  T          111 o
4   |D         31  |_         58  :          85  U          112 p
5   |E         32  <SPACE>    59  ;          86  V          113 q
6   |F         33  !          60  |<         87  W          114 r
7   |G         34  "          61  =          88  X          115 s
8   |H         35  #          62  |>         89  Y          116 t
9   |I         36  $          63  ?          90  Z          117 u
10  |J         37  %          64  @          91  [          118 v
11  |K         38  &          65  A          92  \          119 w
12  |L         39  '          66  B          93  ]          120 x
13  |M         40  (          67  C          94  ^          121 y
14  |N         41  )          68  D          95  _          122 z
15  |0         42  *          69  E          96  £          123 {
16  |P         43  +          70  F          97  a          124 |
17  |Q         44  ,          71  G          98  b          125 }
18  |R         45  -          72  H          99  c          126 ~
19  |S         46  .          73  I          100 d          127 |?
20  |T         47  /          74  J          101 e          128 |!|@
21  |U         48  0          75  K          102 f          129 |!|A
22  |V         49  1          76  L          103 g          .   . 
23  |W         50  2          77  M          104 h          .   . 
24  |X         51  3          78  N          105 i          .   . 
25  |Y         52  4          79  O          106 j          254 |!~
26  |Z         53  5          80  P          107 k          255 |!|?
```

#### 6.3.2.2 Creating the Banner File
To create suitable files, there are 3 possible methods:

* 1. Use the ***BUILD** command (documented in Section 6.6). This is the simplest method, but does not allow a single line with more than 255 characters. If this is going to be a problem, then use method 2 or 3.
* 2. Write a short BASIC program that calls ***SPOOL <file name>**, then outputs the required text using PRINT, then closes the file using ***SPOOL** on its own. For example:
```
        10 *SPOOL BannerFile
        20 PRINT "|L<BANNER>|N<USERNAME>    <USERNAME>     <USERNAME>     <USERNAME>     <USERNAME> |M|J";
        30 PRINT "<START><H>:<M>:<S> on the <DATE><ST> of <MONTHNAME> 19<YEAR>|T|M|J";
        40 *SPOOL
```
This program will generate a banner file containing the text in the example below.
* 3. Use a word processor, for example Wordwise or Edit. Do not use a WYSIWYG (What You See Is What You Get) word processor like  Acornsoft View, because this generates invisible 'control' characters in the text, which will have unexpected effects on the printer.

We recommend that you do not use the automatic line-feed option available on most printers. If the printer always does a line feed when it receives a carriage return character, then users do not have the option of over-printing lines if they wish. In addition, it will not be possible to print files generated by ***SPOOL** without double-spacing. (See description of ***PRINTOUT** command in Section 3.2)

#### 6.3.2.3 Example
A banner file containing this text will cause the user identifier to be printed in bold 5 times at the head of the print output, followed by the date and time at which the printing was, started by the user. At the end of the user's output, a single page throw (Ctrl-L) will appear.
```
|L<BANNER>|N<USERNAME>     <USERNAME >     <USERNAME>    <USERNAME
>     <USERNAME> |M|J<START><H>:<M>:<S> on the <DATE><ST> of <MONT
HNAME> 19<YEAR>|T|M|J
```
The control codes shown are suitable for an Epson printer: |N means 'start double sized text' and |T means 'start normal text'. If your printer has the auto-line-feed option turned on, omit the |J (line-feed) characters from the file.

There are two banners supplied as standard: these are in a directory called **BANNERS** in the root directory   $. The file **$.BANNERS.SIMPLE** contains the following text:
```
|L<BANNER>SJ Research File Server *** Station <STATION> (<USERNAME
>)<DATE><MTH><YEAR> <HOURS>: <MINUTES>: <SECONDS> ***|M| |J
```
which will print the banner shown as an example in Section 6.1, and a single page throw at the end of the user's output. The other banner supplied is called **$.BANNERS.FANCY**, and contains the following text:
```
|J|J|J<MARK><USERNAME><TAB 11>****** Print started at <START><H>:<
M>:<S> <DATE><MTH><YEAR> ******   <USERNAME>|J<MARK><USERNAME><TAB
 11>****** Print ended at   <END><H>:<M>:<S> <DATE><MTH><YEAR>****
**   <USERNAME>|L<BANNER><MARK><USERNAME><TAB 17><USERNAME><TAB 34
><USERNAME><TAB 51><USERNAME><TAB 68><USERNAME>|J*****************
************ SJ Research Printer Server **********************|J<M
ARK>** Output from Station <STATION> (<USERNAME>) at <12HOURS>:<MI
NUTES> <AM> on <DATE><ST> <MONTHNAME> 19<YEAR><TAB 77>**|J********
******************************************************************
*****|J
```
This will print a banner of the form
```
FRED            FRED            FRED           FRED           FRED
******************** SJ Research Printer Server ******************
** Output from Station 068 (FRED) at 3:46 PM ON 2nd August 1986 **
******************************************************************
```
user's text
```
FRED     ****** Print started at 15:46:27  22aug85 ******     FRED
FRED     ****** Print ended at 15:48:17    22aug85 ******     FRED
```
followed by a page throw.

## 6.4 Remote despooler (optional software)
As previously mentioned in this section it is possible for print jobs to be held in the print queue by setting **printing enabled** to **No**. This allows a BBC microcomputer, running the remote despooler software, to take the data and print it out for itself. This has two advantages, first the software allows a station from a different room to print the output, second it allows more than two spooling printers on the network
increasing the throughput.

For the remote despooler to share jobs with the despooler in the fileserver the **Printer exists** option must be set to **Yes**. This will allow the fileserver to despool the contents of its print queue as normal, but if more that one item is held in the print queue then the remote despooler will print it.

The remote despooler software allows a user to specify which names to search for and which type of printer to send to. The program prompts for a logical printer name and then the type of printer. For the type of
printer the program expects a number in the range 0 to 4 corresponding to the value given to ***FX 5,n**.

Despooler software below version 0.10 does not support despooling of more than one logical printer and will only print to the currently selected printer.


Issue 16 Apr 1987
**SJ**research 

