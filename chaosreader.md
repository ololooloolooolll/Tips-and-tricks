# Chaosreader

Chaosreader is a cli tool that will sleuth through a pcap and extract anything it can from files out of http transfers to passwords out of telnet sessions

**Run the tool in a dedicated dump directory as it will create many, many, many files.**

It creates a nice report called index.html

```
chaosreader --help
Version 0.95i, 14-Apr-2014

USAGE: chaosreader [-adehiknqrvxAHIRTUXY] [-D dir]
                   [-b port[,...]] [-B port[,...]]
                   [-j IPaddr[,...]] [-J IPaddr[,...]]
                   [-l port[,...]] [-L port[,...]] [-m bytes[k]]
                   [-M bytes[k]] [-o "time"|"size"|"type"|"ip"]
                   [-p port[,...]] [-P port[,...]]
                   infile [infile2 ...]

       chaosreader -s [mins] | -S [mins[,count]]
                   [-z] [-f 'filter']

   chaosreader           # Create application session files, indexes

   -a, --application     # Create application session files (default)
   -d, --preferdns       # Show DNS names instead of IP addresses
   -e, --everything      # Create HTML 2-way & hex files for everything
   -h                    # Print a brief help
   --help                # Print verbose help (this) and version
   --help2               # Print massive help
   -i, --info            # Create info file
   -q, --quiet           # Quiet, no output to screen
   -r, --raw             # Create raw files
   -v, --verbose         # Verbose - Create ALL files .. (except -e)
   -x, --index           # Create index files (default)
   -A, --noapplication   # Exclude application session files
   -H, --hex             # Include hex dumps (slow)
   -I, --noinfo          # Exclude info files
   -R, --noraw           # Exclude raw files
   -T, --notcp           # Exclude TCP traffic
   -U, --noudp           # Exclude UDP traffic
   -Y, --noicmp          # Exclude ICMP traffic
   -X, --noindex         # Exclude index files
   -k, --keydata         # Create extra files for keystroke analysis
   -n, --names           # Include hostnames in hyperlinked HTTPlog (HTML)
   -D dir    --dir dir        # Output all files to this directory
   -b 25,79  --playtcp 25,79  # replay these TCP ports as well (playback)
   -B 36,42  --playudp 36,42  # replay these UDP ports as well (playback)
   -l 7,79   --htmltcp 7,79   # Create HTML for these TCP ports as well
   -L 7,123  --htmludp 7,123  # Create HTML for these UDP ports as well
   -m 1k     --min 1k         # Min size of connection to save ("k" for Kb)
   -M 1024k  --max 1k         # Max size of connection to save ("k" for Kb)
   -o size   --sort size      # sort Order: time/size/type/ip (Default time)
   -p 21,23  --port 21,23     # Only examine these ports (TCP & UDP)
   -P 80,81  --noport 80,81   # Exclude these ports (TCP & UDP)
   -s 5      --runonce 5      # Standalone. Run tcpdump/snoop for 5 mins.
   -S 5,10   --runmany 5,10   # Standalone, many. 10 samples of 5 mins each.
   -S 5      --runmany 5      # Standalone, endless. 5 min samples forever.
   -z        --runredo        # Standalone, redo. Rereads last run's logs.
   -j 10.1.2.1  --ipaddr 10.1.2.1    # Only examine these IPs
   -J 10.1.2.1  --noipaddr 10.1.2.1  # Exclude these IPs
   -f 'port 7'  --filter 'port 7'    # With standalone, use this dump filter.

eg1,
     tcpdump -s9000 -w output1          # create tcpdump capture file
     chaosreader output1                # extract recognised sessions, or,
     chaosreader -ve output1            # gimme everything, or,
     chaosreader -p 20,21,23 output1    # only ftp and telnet...
eg2,
     snoop -o output1                   # create snoop capture file instead
     chaosreader output1                # extract recognised sessions...
eg3,
     chaosreader -S 2,5         # Standalone, sniff network 5 times for 2 mins
                                # each. View index.html for progress (or .text)
                                
```
