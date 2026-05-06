# OS Lab Manual 09 (1)

## Page 1

                   
 CL-2006  Operating  System  Lab  
 LAB  -09  Mutexes  and  Semaphores  
 
National  University  of  Computer  and  Emerging  Science  Spring  2026

## Page 2

        
Table  of  Content    Objective ....................................................................................................................................... 3 Mutexes ........................................................................................................................................ 3 Applications  of  Mutexes: .......................................................................................................... 3 Introduction  to  Process  Synchronization ................................................................................. 4 Concept  of  Semaphores ............................................................................................................. 5 Implementation  of  Semaphores ................................................................................................. 5 Process  Synchronization  Problem:  Sleeping  Barbar  Problem ............................................... 8 Lab  Activity ................................................................................................................................. 11

## Page 3

Objective  
The  objective  of  this  lab  is  to  study  process  synchronization.  We  will  see  the  concept  of  
semaphores
 
and
 
how
 
we
 
can
 
implement
 
this.
 
We
 
will
 
study
 
process
 
synchronization
 
problems
 
and
 
we
 
will
 
see
 
the
 
sleeping
 
barber
 
problem.
 
 
Mutexes  
Mutex,  short  for  mutual  exclusion,  is  a  synchronization  primitive  used  to  ensure  that  only  one  
thread
 
at
 
a
 
time
 
can
 
access
 
a
 
shared
 
resource.
 
Mutexes
 
are
 
commonly
 
employed
 
in
 
multithreaded
 
programming
 
to
 
prevent
 
race
 
conditions,
 
where
 
multiple
 
threads
 
try
 
to
 
access
 
a
 
shared
 
resource
 
simultaneously,
 
leading
 
to
 
unpredictable
 
behavior.
 
Applications
 
of
 
Mutexes:
 
 ●  Protecting  Critical  Sections:  Mutexes  are  used  to  protect  critical  sections  of  code,  
ensuring
 
that
 
only
 
one
 
thread
 
can
 
execute
 
the
 
code
 
block
 
at
 
a
 
time.
 
This
 
prevents
 
data
 
corruption
 
and
 
maintains
 
consistency
 
when
 
multiple
 
threads
 
access
 
shared
 
data.
 ●  Thread  Synchronization:  Mutexes  are  essential  for  synchronizing  access  to  shared  
resources
 
such
 
as
 
variables,
 
data
 
structures,
 
or
 
files
 
in
 
a
 
multithreaded
 
environment.
 ●  Resource  Management:  Mutexes  are  used  to  coordinate  access  to  resources  that  can  
only
 
be
 
used
 
by
 
one
 
thread
 
at
 
a
 
time,
 
such
 
as
 
hardware
 
devices
 
or
 
database
 
connections.

## Page 4

 
  
Introduction  to  Process  Synchronization
 
When  processes  cooperate  to  perform  a  task,  they  need  to  communicate  on  a  shared  medium.  
Usually
 
this
 
shared
 
medium
 
is
 
some
 
resource
 
allocated
 
to
 
any
 
of
 
the
 
processes
 
cooperating.
 
When
 
more
 
than
 
one
 
process
 
tries
 
to
 
write
 
on
 
it,
 
this
 
causes
 
concurrency
 
control
 
problems
 
since
 
if
 
two
 
or
 
more
 
processes
 
are
 
able
 
to
 
write
 
the
 
shared
 
medium
 
simultaneously,
 
then
 
there
 
is
 
a
 
strong
 
chance
 
that
 
the
 
data
 
becomes
 
inconsistent.
 
To
 
avoid
 
this
 
concurrency
 
control
 
problem,
 
we
 
often
 
allow
 
processes
 
to
 
lock
 
the
 
resources
 
in
 
order
 
to
 
avoid
 
simultaneous
 
access.
 
There
 
are
 
two
 
types
 
of
 
locks:
  
 ●  Shared  lock  (used  for  reading  purposes)    ●  Exclusive  lock  (used  for  writing  purposes)   With  shared  lock  more  than  one  reading  process  can  be  in  a  critical  section  of  the  code  where  
they
 
access
 
the
 
shared
 
resource,
 
whereas
 
in
 
exclusive
 
lock,
 
not
 
more
 
than
 
a
 
single
 
process
 
is
 
allowed
 
to
 
access
 
the
 
resource.
 
Mutual
 
Exclusion
 
as
 
you
 
may
 
have
 
studied
 
in
 
theory
 
class,
 
is
 
used
 
to
 
enforce
 
the
 
process
 
concurrency
 
control
 
avoiding
 
deadlock
 
conditions.
 
Today
 
our
 
task
 
is
 
to
 
study
 
the
 
usage
 
of
 
semaphores.

## Page 5

Concept  of  Semaphores
 
A  semaphore  is  a  counter  that  can  be  used  to  synchronize  multiple  threads.  Linux  guarantees  
that
 
checking
 
or
 
modifying
 
the
 
value
 
of
 
a
 
semaphore
 
can
 
be
 
done
 
safely,
 
without
 
creating
 
a
 
race
 
condition.Each
 
semaphore
 
has
 
a
 
counter
 
value,
 
which
 
is
 
a
 
non-negative
 
integer.
 
A
 
semaphore
 
supports
 
two
 
basic
 
operations:
 
 ●  A  wait  operation  decrements  the  value  of  the  semaphore  by  1.  If  the  value  is  already  
zero,
 
the
 
operation
 
blocks
 
until
 
the
 
value
 
of
 
the
 
semaphore
 
becomes
 
positive
 
(due
 
to
 
the
 
action
 
of
 
some
 
other
 
thread).
 
When
 
the
 
semaphore’s
 
value
 
becomes
 
positive,
 
it
 
is
 
decremented
 
by
 
1
 
and
 
the
 
wait
 
operation
 
returns.
  
 ●  A  post  operation  increments  the  value  of  the  semaphore  by  1.  If  the  semaphore  was  
previously
 
zero
 
and
 
other
 
threads
 
are
 
blocked
 
in
 
a
 
wait
 
operation
 
on
 
that
 
semaphore,
 
one
 
of
 
those
 
threads
 
is
 
unblocked
 
and
 
its
 
wait
 
operation
 
completes
 
(which
 
brings
 
the
 
semaphore’s
 
value
 
back
 
to
 
zero).
 
 There  are  two  types  of  semaphores:  ●  Named  semaphores  are  powerful  semaphores  that  are  usually  created  to  share  among  
processes
 
running
 
from
 
different
 
files.
 
This
 
type
 
of
 
semaphore
 
creates
 
a
 
temporary
 
file
 
under
 
the
 
directory
 
/temp,
 
that
 
stores
 
the
 
value
 
of
 
semaphore.
 
 ●  Unnamed  semaphores  are  less  powerful  semaphores  that  often  work  in  a  single  file,  
they
 
have
 
no
 
presence
 
outside
 
the
 
file
 
  
Implementation  of  Semaphores  
A  semaphore  is  represented  by  a  variable  whose  type  is  ‘sem_t’  and  is  defined  in  ‘semaphore.h’  
library,
 
the
 
following
 
are
 
some
 
basic
 
routine
 
calls
 
related
 
to
 
semaphores.
 
  
S.  No   Functions   Description  
1  sem_init()  Initialize  an  unnamed  semaphore   
2  sem_destroy()  Destroy  an  unnamed  semaphore   
3  sem_wait()  Locks  the  semaphore  referenced  by  sem_t  by  performing  a  semaphore  lock  operation  on  that  semaphore   
4  sem_post()  Unlocks  a  semaphore   
 
The  semaphores  use  semaphore.h  to  define  the  required  data  structures  and  functions.  Some  
of
 
them
 
are
 
defined
 
in
 
pthread.h
 
as
 
well,
 
so
 
at
 
times
 
semaphore
 
programs
 
give
 
undefined
 
reference
 
error
 
to
 
sem_wait
 
and
 
sem_post.
 
If
 
you
 
happen
 
to
 
encounter
 
this
 
problem,
 
try
 
adding
 
pthread.h
 
and
 
compiling
 
it
 
as:
 
  
gcc  -o  output  -pthread  source.   
 
The  ‘sem_init()’  initializes  an  unnamed  semaphore,  the  definition  of  this  routine  call  is  given  
below:

## Page 6

sem_t  sem;   int  sem_init(sem_t  *sem,  int  p  shared,  unsigned  int  value)   
 
The  above  initializes  unnamed  semaphore  referenced  to  sem  by  the  value.  P  shared  indicates  
whether
 
the
 
semaphore
 
is
 
shared
 
among
 
the
 
processes
 
(pshared
 
is
 
zero
 
the
 
semaphore
 
is
 
not
 
shared
 
otherwise
 
shared).
 
Returns
 
0
 
if
 
success
 
otherwise
 
-
 
1.
  
int  sem_wait(sem_t  *sem)   
 
if  the  value  of  semaphore  is  greater  than  zero,  sem_wait()  will  immediately  decrease  it  by  1  and  
return.
 
Otherwise
 
the
 
process
 
is
 
blocked.
 
This
 
function
 
returns
 
0
 
if
 
success
 
and
 
-1
 
when
 
error.
 
  
int  sem_post(sem_t  *sem)   
 
Increments  the  value  of  the  semaphore  by  1  pointed  by  the  sem_t.  If  the  value  becomes  greater  
than
 
zero
 
the
 
process
 
is
 
unblocked.
 
Returns
 
0
 
on
 
success
 
and
 
-1
 
on
 
error.
 
  
int  sem_destroy(sem_t  *sem)   
 
Destroys  an  unnamed  semaphore  pointed  by  the  variable  sem_t,  if  there  is  a  process  waiting  for  
this
 
semaphore
 
or
 
the
 
semaphore
 
is
 
already
 
destroyed.
 
The
 
program
 
may
 
produce
 
undefined
 
behavior.
 
This
 
function
 
returns
 
0
 
if
 
success
 
or
 
-1
 
if
 
error.
 
The
 
below
 
code
 
demonstrates
 
the
 
use
 
of
 
semaphore
 
in
 
a
 
counter
 
variable
 
in
 
a
 
multithreaded
 
environment.

## Page 7



## Page 8

 
  
Process  Synchronization  Problem:  Sleeping  Barbar  Problem

## Page 9



## Page 10



## Page 11

Lab  Activity  
1.  Implement  both  below  parts:  ●  Create  an  ice  cream  eating  contest  problem  protected  by  a  semaphore  lock.  Use  
global
 
variables
 
icecreamremaining.
 
Create
 
3
 
threads
 
for
 
3
 
persons
 
to
 
eat
 
icecreams
 
until
 
all
 
are
 
finished.
 
But
 
only
 
one
 
person
 
will
 
be
 
given
 
ice
 
cream
 
at
 
a
 
time
 
by
 
the
 
salesman.
 
So
 
restrict
 
access
 
to
 
icecreams
 
so
 
that
 
only
 
one
 
thread
 
can
 
decrement
 
it
 
by
 
using
 
a
 
semaphore.
 
So
 
use
 
sem_wait
 
and
 
Sem_post
 
in
 
thread.
 
 ●  Get  each  person  to  count  money  from  his  wallet  for  the  icecream  payment  which  
can
 
take
 
one
 
to
 
2
 
seconds
 
during
 
which
 
another
 
person
 
can
 
acquire
 
the
 
salesman
 
to
 
sell
 
him
 
ice
 
cream.
 
Redo
 
the
 
coding
 
to
 
accommodate
 
this
 
condition
 
in
 
your
 
threads
 
as
 
well.
 
 2.  You  need  to  synchronize  customers  at  the  boarding  lounge  of  an  airport  using  
semaphore.
 
where
 
there
 
are
 
10
 
customers,
 
each
 
needs
 
to
 
weigh
 
his
 
luggage,
 
get
 
it
 
checked
 
and
 
get
 
a
 
boarding
 
pass.
 
During
 
each
 
task
 
passengers
 
are
 
too
 
bored
 
that
 
they
 
sleep,
 
weighting
 
luggage
 
takes
 
4
 
seconds
 
sleep,
 
security
 
check
 
for
 
luggage
 
needs
 
7
 
seconds
 
sleep
 
and
 
getting
 
boarding
 
pass
 
needs
 
3
 
seconds
 
sleep
 
 3.  Create  two  threads  that  increment  a  global  counter  1000  times  each.  Use  a  mutex  to  
avoid
 
race
 
conditions
 
and
 
print
 
the
 
final
 
result.
