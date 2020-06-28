## DAPL   

I Spent quite a while writing the __Data Analyst Programming Language__. It's supposed to make life a bit easier 
when your looking for interesting patterns of activity in things like Web logs Etc. The whole idea seems to have 
fallen on deaf ears (maybe because it's no good, or maybe because the 
[_target audience_](https://wiki.openrightsgroup.org/wiki/Cyber_Specials "Cyber Police volunteers - but because 
it's a new line of work for the Police, all the volunteers have given up trying") couldn't see past the end of 
their noses), but I've left the code around just in case anyone shows any interest. Have a look at the repository 
[_here_](https://github.com/wicked-rainman/DAPL "Go on, click it. You know you want to!") if you are interested.   


### OVERVIEW

DAPL is a program language wrapper intended to simplify the process of analysing large volumes of structured 
single-line records (for example HTTP, SSH and Audit logs, phone or building access logs and the like). 
The wrapper might be thought of as mysql for CSV files, but without the databases, or perhaps the query language 
components of Model 204. The underlying language is C and has only been tested on modern versions of Fedora. The primary 
focus in all this work has been to keep things small, lean and simple.

Provisions are made for dealing with other forms of data through a conversion process 
(Currently only one such converter exists - for processing spam E-mail). 

A small range of standalone utilities that aid dealing with IP related data have been included, albeit they are 
separate (but replicated) from the core DAPL wrapper. Data "fusion" can take place through inbuilt lookup functions
that read separate reference files. 

All of this functionality is created using old-fashioned procedural programming techniques. There ain't no Rumbaugh here.

DAPL makes provisions for two code blocks within any main routine:

### setup():
Code within the setup block is executed once after program initialisation. It's purpose is to 
allow the user to perform startup functions like opening input and output files, defining input 
fields, identifying reference files Etc. Any failures within the setup block stops the whole process 
running. The user is shielded from the complexities of performing these operations through the use
of high level function calls.  

### loop()  

Code within the loop block is executed once for each record contained in each input file identified 
in setup(). A User-obscured global data structure is created for each record, populated with the fieldname 
and field value pairs found. All functions within the loop block reference this structure. Once the record 
has been processed it is reset to empty, ready to be populated with the fields from the next record. 
    
Other than maintaining a count of input and output records and maintaining file or memory pointers for any 
reference files, there is no state within the code block. This allows for processing of undefinably 
large volumes of input, restricted only by the memory requirements for holding one single record at a time.  

Code within the loop block is generally fault tollerant. For example, function references to field names 
that are non-existant in the input result in the calling function failing gracefully (This allows for the 
successful processing of files that have different fields - where not all of the fields in one are present 
in the other).  

Loop functions tend to fall into one of three categories:

-        Those that Enable the selection or rejection of individual records, based on
         string matching, substring matching or through regular expression pattern matching. 
         Rejected records are internally assigned a "drop" flag. If a drop flag is 
         present, all sequentially following loop functions will exit without performing their 
         intended actions (I.E, the record is ignored). Early rejection of unwanted records can 
         obviously dramatically improve processing times.
         
-        Value editing functions that can replace, sanitse, substring or add to the underlying
         data in some way. Field values can be looked up in locally held tables, or from external
         sources via socket calls with suitable APIs. Field values can be combined or added to in order
         to make them unique (such as adding DTGs Etc). 
         
-        Graphical data modeling. Relationships between data fields can be defined and visualised
         by generating .dot output that can be rendered by graphviz in various ways (such as SVG, PDF 
         JPEG Etc). Duplicate relationships are set to be effectively de-duped by the .dot processor, 
         making large volumes of data easier to analyse.
         
Sample code can be found in the ./example_code directory, together with sample data in ./input and results
in ./output. This may aid with the learning process. 

A brief description of the utilities/files produced by the included Makefile can be found in ./docs/Manifest.md. 
See INITIAL INSTALL section below.

----------------------------------------------------------------------------------------------

## FURTHER READING

- Graphviz        - https://graphviz.org
- Detox           - http://detox.sourceforge.net
- msgconvert      - https://github.com/mvz/email-outlook-message-perl
- abuseip         - https://www.abuseipdb.com/api.html
- Reverse DNS     - https://opendata.rapid7.com/sonar.rdns_v2/
- DNS             - https://opendata.rapid7.com/sonar.fdns_v2/
- Topology        - http://www.caida.org/data/active/ipv4_routed_24_topology_dataset.xml
- AbuseIPdb       - https://www.abuseipdb.com/
        
------------------------------------------------------------------------------------------------

## INSTALL

1.  cd into your $HOME directory

2.  Clone the repository using `git clone https://github.com/wicked-rainman/DAPL.git`. This should create a 
directory named "DAPL".

3.  cd into $HOME/DAPL/src

4.  As root, run `./Configure` to make sure system dependancies are present. GCC and Graphviz are critical for 
DAPL. Openssl-dev is needed for the  sslcat and abuseipdb standalone utilities, detox, dos2unix and the perl 
script msgconvert are needed for any E-mail processing.

5.  exit root and as a user run `make`. You shouldn't see any errors, but you will see a few warning messages
about unused variables (These variables have been intentional left for any future debugging purposes and do
no harm).

6.  DAPL can be run as a client or as a server. For the client install, run`sudo make Client` or for the server 
(if you are happy with what actions it is going to perform),`sudo make Server`. If you plan to have a complete 
client and server install, repeat step 5 again before running the next make Server or make Client.

7. After a server install, use systemctl to start and enable gasnd.service, gdnsd.service, grdnsd.service, 
ghistory.service and gcountryd.service as required. Ensure that the TCP ports specified in the bash 
scripts gasnd, gdnsd, grdnsd, gcountryd and ghistoryd (/usr/local/sbin) are allowed through any firewall.
_(Note that some of these scripts also have BASH variables that point to data reference files - they will almost 
certainly have to be modified to suit your filesystem)._ 

8. In a client install, Edit $HOME/.bashrc, and add these BASH variables:

        WHITE_FILE=$HOME/DAPL/Reference/whitelist.csv; export WHITE_FILE
        ASN_FILE=$HOME/DAPL/Reference/asn.csv; export ASN_FILE
        COUNTRY_FILE=$HOME/DAPL/Reference/country.csv; export COUNTRY_FILE
        GDNS_PORT=32481; export GDNS_PORT
        GASN_PORT=32482; export GASN_PORT
        GCOUNTRY_PORT=32483; export GCOUNTRY_PORT
        GRDNS_PORT=32484; export GRDNS_PORT
        GHISTORY_PORT=32485; export GHISTORY_PORT
        GSERVER=127.0.0.1; export GSERVER
        
The ASN_FILE, COUNTRY_FILE and WHITE_FILE files are used within DAPL (functions add_asn(), add_country() 
and whitelist() ) for local resolution and provide non-server related answers. 

DAPL functions socketadd_asn() socketadd_country() and socketadd_history() will resolve answers through 
the related server ports. DAPL functions socketadd_dns() and socketadd_rdns() have not been written yet, 
(see open issues) although Standalone utilities gdns grdns reference these other ports. 

9. Create any user programs in $HOME/DAPL/progs. To compile each program, use the command:
`gcc -Ofast prog.c ../lib/libdapl.a -o progname` for files conaining single line "CSV" type records, or
`gcc -Ofast prog.c ../lib/libeml.a -o progname` to utilise the E-mail conversion handler

10. On a client, any additional reference files you make should reside in $HOME/DAPL/Reference. 

11. On a Server, DNS related files must all be built from scratch using the DNS related scripts in sbin - dns_auth_update() 
and rdns_update(). Have a look in the ./docs directory for a bit of steerage.

