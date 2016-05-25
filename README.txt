README.txt

How to use outgoing_admin scripts
################################################################################

To prepare a directory to return to someone.

### Summary ###

The directory you want to send to a client should have a unique name with 
no spaces in it.

Something like 

Clients_Name_Analysis

and not something generic like

Analysis

You need a path to this directory (see instructions below), as well as the 
client's first and last name and their email address. 

Then do this:

cd /data/WHRI-GenomeCentre/outgoing_admin/scripts

# to get a reminder of how to use handbackData, type:
./handbackData  

# to prepare a directory and add it to the outgoing directory and the email 
#queue, type:
./handbackData -d <path_to_directory> -f <clients_first_name> -l <clients_last_name> -e <clients_email>

# and replace text inside < > with the values you want to use.  
# It might be easiest to prepare the command in a text editor first so you can check it.

#In the example given below, you would type
#./handbackData -d /data/WHRI-GenomeCentre/shares/Projects/Illumina_Projects/SNP_Genotyping/Kimberley_Christopher/GC-CK-5574/Christopher_Analysis -f Christopher -l Kimberley -e c.kimberley@qmul.ac.uk

### Detailed instructions and notes ###

1. Get the path to the directory that you want   

Locate the directory on the bash command line.  For example, if we change to the 
directory that contains the directory that we want to send by typing this:

cd /data/WHRI-GenomeCentre/shares/Projects/Illumina_Projects/SNP_Genotyping/Kimberley_Christopher/GC-CK-5574/

and get a listing of its contents

ls -l 

total 880992
drwxrwx---+ 3 wgw027 qmul       512 Apr 28 14:31 Analysis
-rwxrw----+ 1 wgw027 qmul 902126564 May 17 15:10 Analysis.zip
drwxrwx---+ 4 wgw027 qmul       512 Apr 25 11:48 Data
drwxrwx---+ 3 wgw027 qmul       512 Apr 26 09:47 Process


And if the "Analysis" directory is the one that we want to tarball and send 
to the client, then the path we need is

/data/WHRI-GenomeCentre/shares/Projects/Illumina_Projects/SNP_Genotyping/Kimberley_Christopher/GC-CK-5574/Analysis

but it would probably be better to first rename the directory to something more unique like Christopher_Analysis:

mv Analysis Christopher_Analysis

and then the path you need for the steps below would be

/data/WHRI-GenomeCentre/shares/Projects/Illumina_Projects/SNP_Genotyping/Kimberley_Christopher/GC-CK-5574/Christopher_Analysis


A few notes:
a) The directory does not have to be compressed.  The script will do the 
compression for you and check that the compression succeeded.  It does not 
hurt if the directory is compressed or contains compressed files; it just 
means more work for the client when they are unpacking their data - they
will have to do more than one decompression.
b) The path needs to have forward-slashes in it not the backward slashes 
used by Windows and Dos.
c) The path needs to be a "full-path".  This means it has to start with 
/data/WHRI-GenomeCentre.  If you cannot type

cd <some path>

and see the content you intend to send (using an ls command), then the 
script will not work.

2. You also need to know the recipients first and last name and email address.
In this case they are:

Firstname: Christopher
Last name: Kimberley
Email: c.kimberley@qmul.ac.uk

3. Change to the outgoing admin directory:

cd /data/WHRI-GenomeCentre/outgoing_admin/scripts

4. Execute the command

./handbackData -d /data/WHRI-GenomeCentre/shares/Projects/Illumina_Projects/SNP_Genotyping/Kimberley_Christopher/GC-CK-5574/Analysis -f Christopher -l Kimberley -e c.kimberley@qmul.ac.uk

5. If you make a mistake entering the above command, you may receive an error 
message.  Correct any mistakes and try again.

6. If all goes well you will see output to screen confirming what is to 
be done, a listing of files as they are being compressed, and finally,
lines containing the text:

Analysis was successfully moved to ... 
Analysis was successfully added to the the mandate file: ...
finished preparing Analysis. ...

If you dont see lines, like this, ask for help.

7. What has happened?

The original directory is still there but has been renamed

cd /data/WHRI-GenomeCentre/shares/Projects/Illumina_Projects/SNP_Genotyping/Kimberley_Christopher/GC-CK-5574
ls -l
total 880992
drwxrwx---+ 3 wgw027 qmul       512 Apr 28 14:31 Analysis.canBeDeletedAfterRetrieval
-rwxrw----+ 1 wgw027 qmul 902126564 May 17 15:10 Analysis.zip
drwxrwx---+ 4 wgw027 qmul       512 Apr 25 11:48 Data
drwxrwx---+ 3 wgw027 qmul       512 Apr 26 09:47 Process


A compressed version of the directory is now in the outgoing directory

ls -l /data/WHRI-GenomeCentre/outgoing
 
total 8
drwxrws---+ 2 wgw057 WHRI-GenomeCentre  512 May 10 17:43 AFearon_HumanHT12_051213_Ambion
drwxrws---+ 2 wgw057 WHRI-GenomeCentre  512 May 19 11:16 Analysis
drwxrws---+ 2 wgw057 WHRI-GenomeCentre  512 Apr 26 11:49 Branco_Miguel
drwxrws---+ 2 wgw001 WHRI-GenomeCentre 4096 Feb 25 17:57 ChazFolder
...


An entry has been made in a mandate file that will be used to notify clients once per week
for four weeks of their data package that is to be picked up.

See

less -S /data/WHRI-GenomeCentre/outgoing_admin/mandate/handbackMandate


8. What will happen?

Emails are sent once per week (on Tuesday at 1 PM).  Four emails will be sent 
to the client with instructions on how to retrieve data.  After the fourth week,
the directory will be moved to 

/data/WHRI-GenomeCentre/outgoing_admin/deletion

and the line from the handbackMandate will be removed and added to
the deletionMandate file which can be viewed here

less -S /data/WHRI-GenomeCentre/outgoing_admin/mandate/deletionMandate

Nothing will actually be deleted by any script.  Deletion has to be done by hand
