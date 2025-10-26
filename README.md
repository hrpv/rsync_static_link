# rsync_static_link
Build instructions for a static linked rsync binary.

I had lot of trouble with an old rsync version 3.1.3 
on my Raspberry PI "Raspbian GNU/Linux 10 (buster)" when i installed log2ram.

log2ram uses rsync. A fallback to cp works, but cp copy always the complete files not only deltas

testing of log2ram

### sudo log2ram write 

ends up with random rsync errors, i lost some files because they are not copied

building file list ... done

auth.log
daemon.log
lastlog

rsync: write failed on "/var/hdd.log/lastlog": Success (0)

rsync error: error in file IO (code 11) at receiver.c(374) [receiver=3.1.3]



### Instead of updating the whole system I searched for a static linked binary, but found no working solution

So I had to compile my own static version of rsync

Following the installation instruction

https://github.com/RsyncProject/rsync/blob/master/INSTALL.md



## get rsync
```
git clone https://github.com/RsyncProject/rsync.git

cd rsync

python3 -mpip install --user commonmark #not really necessary

./md-convert --test rsync-ssl.1.md   #The test was successful.

sudo apt install -y gcc g++ gawk autoconf automake python3-cmarkgfm
sudo apt install -y acl libacl1-dev
sudo apt install -y attr libattr1-dev
sudo apt install -y libxxhash-dev
sudo apt install -y libzstd-dev
sudo apt install -y liblz4-dev
sudo apt install -y libssl-dev


#this is  the important step, configure CFLAGS='-static'   


./configure CFLAGS='-static'   --disable-openssl   --disable-xxhash   --disable-zstd   --disable-lz4 


make

#optional strip ./rsync

sudo cp rsync /usr/bin

#ldd ldd /usr/bin/rsync das Programm ist nicht dynamisch gelinkt
```



Retest (more than once)

### sudo log2ram write 

building file list ... done

auth.log
mosquitto/mosquitto.log


sent 70.134 bytes  received 12.043 bytes  54.784,67 bytes/sec

total size is 4.755.062  speedup is 57,86




