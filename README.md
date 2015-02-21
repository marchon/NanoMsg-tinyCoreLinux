# NanoMsg-tinyCoreLinux
Packages for running Nanomsg on Tiny Core Linux

TinyCoreLinux + Nanomsg in 64MB 
--------------------------------------------
This is a test installation of a TinyCoreLinux package
with nanomsg library and compiled nanocat 
--------------------------------------------
g0t TinyCoreLinux? Try it instantly!

wget http://www.lazarusco.in/nanomsg-tcz/nanomsg.tcz

tce-load -w -i nanomsg.tcz

nanocat --rep --bind tcp://127.0.0.1:1234 --data pong --format ascii
nanocat --req --connect tcp://127.0.0.1:1234 --data ping--format ascii



In this repo are the files and installation proces to build 
this package yourself. 

The dev package downloads the c-compiler - libraries - sourcecode - 
and build instructions for you  

If you are unfamiliar with Either Tiny Core Linux or Nanomsg look at this

Tiny Core Linux - a 10mb linux distribution that runs in memory
     http://www.tinycorelinux.net/

NanoMsg - a high performance message queueing engine
     http://nanomsg.org

nanocat - a command-line interface to nanomsg


Test Cases for Nanomsg using nanocat from the command line. 

The ping-pong with nn_req/nn_rep sockets (must be run simultaneously):

nanocat --rep --bind tcp://127.0.0.1:1234 --data pong --format ascii
nanocat --req --connect tcp://127.0.0.1:1234 --data ping--format ascii

Or in shorter to write form:

nn_rep -L1234 -Dpong -A
nn_req -l1234 -Dping -A

Do periodic requests once a second:

nn_req -l1234 -Dping -A -i 1

The rep socket that never reply (no -D option), may be used to check if resending the requests is actually work:

nanocat --rep --connect ipc:///var/run/app/req.socket

Send an output of the ls to whatever would connect to 127.0.0.1:1234 then exit:

ls | nanocat --push -L1234 -F-
Send heartbeats to imaginary monitoring service:

nanocat --pub --connect tpc://monitoring.example.org -D"I am alive!" --interval 10



http://nanomsg.org/v0.2/nanocat.1.html
