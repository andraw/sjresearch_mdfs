# Chapter 1: Introduction to the SJ Research File Server

## 1.0 How to use this Manual

This manual is split into sections covering different aspects of operation of the File Server, as follows

Section| Title | Chapters
-----------|----------------------|---------------------------
Section A  | Introduction         | Chapter 1
Section B  | For Users            | Chapter 2, Chapter 3
Section C  | For System Managers  | Chapter 4, Chapter 5, Chapter 6, Chapter 7, Chapter 8, Chapter 9
Section D  | For Programmers      | Chapter 10
Appendix A | Error Messages given by BBC Computers
Appendix B | System Errors
Appendix C | Installing Your System


The rest of this chapter gives an overall description of the SJ Research File Server system.

## 1.1 Introduction to the SJ Research File Server Systems
The SJ Research Modular Disc File Server is designed to work on Econet® local area computer networks, to the specification laid down by Acorn Computers Ltd as "Econet Level 2" but with a number of additional features. The full features of the SJ Research systems are briefly described below:

* Fully *random access* to files is offered, either one byte at a time, or a specified block of data (up to the entire file) at a time.
* The concept of *fileowners* (with passwords if required) is offered to restrict access to files by unauthorised users.
* Fileowners’ directories are themselves files (of a special sort) so that a fileowner can have sub—directories within other directories. In addition, the *root* directory of the system shall be accessible to users, allowing them to access (where authorised) files belonging to other fileowners.
* The Modular Disc File Server allows four floppy disc drives and up to two hard discs (up to 140 megabytes). The MDFS stores data, on the floppy disc drives, using double density, which means that on each standard 80 track disc drive *800 kilobytes* (K) of data can be stored.
* In addition, the MDFS supports a tape streamer for backing up hard discs. This allows important data to be protected, off-site if need be; data can also be interchanged on this medium.
* As the MDFS can use both hard discs and floppy discs this allows the hard disc to be used for general purpose software whilst the floppy disc can contain software specific to a particular group of people.
* A system of *accounts* is provided, to control both the use of disc space by users, and owner access to files. Each fileowner is allocated one or more accounts, and each account is given a *balance* by the person in charge of the system (the System Manager). Account numbers range between 0 and FF (hexadecimal), although the system manager could of course use 0 to 99 if thisIS simpler. By allocation of a suitable balance to each account, users can be encouraged to remove unwanted files.
* The account number given to a file controls the *owner access* to the file, that is to say, the user with access to the account number of a file may read, write or delete that file; if the file is a directory, he may create new files in that directory.
* Each file has also an *auxiliary account number*. This can be set by the fileowner. The user(s) with access to the account with number equal to the file’s auxiliary account number, also has owner access to that file.
* If an attempt is made to load or open any file that is not in the currently selected directory, the *library directory* will be searched for the file. This will occur regardless of the method of access to the file (Level 2 specifies this feature only for * commands). When a user logs-on, the file server will automatically select the directory LIBRARY (if it exists) as library directory.
* A *real-time* clock is included in the File Server. When the full information about a file is requested, the system will display the date of first creation of the file, and the date and time that the file was last updated. In addition, utility programs (for example *TIME) are provided to read the clock directly. The clock runs from an internal rechargeable battery when the system is switched off.
* A *printer server* is included in the unit, allowing any station on the network to route its output to a printer, via the network itself.
* The MDFS supports *printer spooling* so that output routed to a busy printer will be stored on disc until the printer becomes free. The print queue is accessible to users, who can thus control the order in which jobs are printed when they have access to appropriate account numbers.

Note that the additional feature of accounts need not affect the ordinary users, unless they specifically wish to make use of them. In fact, the system manager may turn off the accounting system completely where no data security is required: in this case all users would have access to everything on the system. Alternatively, he may keep data security but disable the disc space accounting part of the system, by setting all accounts to a suitably large value. See Section 3.2 (under *ACCOUNT and *ACCESS) for a full description of account control.

Issue 14 Mar 1987
**SJ**research

