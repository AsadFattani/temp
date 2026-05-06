# OS Revision Lab 

## Page 1

               
 CL-2006  Operating  System  Lab  
  
Revision  Lab   
 
National  University  of  Computer  and  Emerging  Science  Spring  2026

## Page 2

Lab  Activity  
1.  Open  a  terminal  and  execute  the  following  tasks:  ●  Create  a  directory  named  ‘your  roll  no’  in  your  home  directory.  ●  Navigate  into  the  newly  created  directory.  ●  Check  if  the  GNU  C++  Compiler  (g++)  is  installed;  if  not,  install  it  using  the  
appropriate
 
package
 
manager
 
command.
 ●  Inside  the  ‘your  roll  no’  directory,  create  a  C++  file  named  ‘RevisionC.cpp’  using  
the
 
touch
 
command
 
and
 
write
 
a
 
program
 
to
 
print
 
prime
 
numbers
 
till
 
n.
 ●  Confirm  the  existence  of  the  ‘RevisionC.cpp’  file  and  display  the  result  after  
successfully
 
compiling
 
the
 
source
 
file.
  2.  In  a  Linux  terminal,  using  a  single  echo  command,  print  the  following  output:  “Welcome  to  Linux,  Linux  is  free,  secure  and  open  source”.  Additionally,  execute  the  following  tasks:  ●  Create  a  folder  named  ‘osRevlab’  on  the  Desktop.  ●  Inside  the  ‘osRevlab’  folder,  include  two  text  files  named  ‘YourFirstName.txt’  and  
‘YourLastName.txt’.
 ●  Generate  a  third  file  named  ‘mergedfile.txt’  within  the  ‘osRevlab’  folder,  and  
ensure
 
that
 
‘mergedfile.txt’
 
contains
 
the
 
combined
 
content
 
of
 
‘YourFirstName.txt’
 
and
 
‘YourLastName.txt’.
 ●  Copy  ‘mergedfile.txt’  to  a  new  file  named  ‘copiedfile.txt’  in  the  ‘osRevlab’  folder.  ●  Delete  all  files  (YourFirstName.txt,  YourLastName.txt,  mergedfile.txt,  
copiedfile.txt)
 
inside
 
the
 
‘osRevlab’
 
folder.
  3.  Perform  the  following  tasks:  ●  Identify  the  command  to  list  files  in  the  current  directory  that  have  names  starting  
with
 
an
 
uppercase
 
letter.
 ●  Create  three  new  directories  named  ‘Reports’,  ‘Projects’,  and  ‘Archive’  using  a  
single
 
command
 
if
 
they
 
don’t
 
already
 
exist.
 ●  Copy  files  in  the  current  directory  containing  the  character  string  ‘report’  into  the  
‘Reports’
 
subdirectory.
 ●  Copy  files  in  the  ‘Reports’  subdirectory  with  names  ending  in  ‘.txt’  or  ‘.docx’  into  
the
 
‘Projects’
 
subdirectory.
 ●  Copy  files  in  the  ‘Projects’  subdirectory  containing  the  character  string  ‘notes’  or  
‘misc’
 
into
 
the
 
‘Archive’
 
subdirectory.
 ●  Copy  files  starting  with  ‘important_’  from  the  ‘Archive’  subdirectory  into  the  
‘Backup’
 
subdirectory.
 
Move
 
files
 
starting
 
with
 
‘obsolete_’
 
from
 
the
 
‘Archive’
 
subdirectory
 
into
 
the
 
‘Backup’
 
subdirectory.
 ●  Delete  all  files  containing  the  sequence  ‘obsolete’  from  the  ‘Backup’  subdirectory.   4.  Write  a  script  that  accepts  a  sentence  and  counts  the  number  of  words  in  it.

## Page 3

5.  Write  a  program  that  reads  a  text  file  named  ‘input.txt’  and  counts  the  number  of  words  
in
 
it.
 
Implement
 
error
 
handling
 
for
 
file
 
opening
 
and
 
reading
 
operations.
 
Utilize
 
open(),
 
read(),
 
and
 
close()
 
system
 
calls.
  6.  Develop  a  program  that  creates  four  child  processes.  Each  child  process  executes  a  different  command-line  utility  (ls,  ps,  whereis,  mkdir)  using  the  execlp()  function.  The  parent  process  waits  for  all  child  processes  to  complete  and  then  prints  a  message  indicating  their  completion.   7.  Develop  a  program  that  writes  a  string  provided  as  a  command-line  argument  to  a  text  
file
 
named
 
‘data.txt’.
 
Implement
 
error
 
handling
 
for
 
file
 
opening
 
and
 
writing
 
operations.
 
Utilize
 
open(),
 
write(),
 
and
 
close()
 
system
 
calls.
  8.  Create  the  following  functions  in  separate  files  (using  .h  and  .c  files)  EvenCount,  
OddCount,
 
TotalCount.
 ●  EvenCount  counts  the  number  of  even  numbers  in  the  list.  ●  OddCount  counts  the  number  of  odd  numbers  in  the  list.  ●  TotalCount  counts  the  total  numbers  in  the  list.  Create  a  list  of  numbers  or  take  it  from  the  user  in  the  main  function.  Now  compile  all  
functions
 
using
 
makefile.
