There are probably only two ways you ended up here in this thread:
1) You were browsing XDA and came across this thread and thought "Hey, that's that? Let's take a look..."
2) You were looking for an iotop port for Android

If 2) applies to you, then the you were doing the exact same this as I was doing some days ago. The only difference is.... when I was searching there was no such port 
But for debugging purposes on my Tab, I needed such a tool. So I started writing my own  


So, in case you're not familiar with iotop, iotop is a tool for examining I/O loads and and I/O usage on per-process basis. It shows the total amount of read and written bytes as well as the current read/write speeds.

First up, the script is not yet as powerful as the one for PCs. It's still WIP but does the main tasks it's supposed to.
If you have an idea and know how to realize it, please feel free to fork my repo and create a pull request. I will most likely be merging it happily.


Requirements:

Root
Kernel with I/O accounting enabled
The following configs must be set:
CONFIG_TASKSTATS
CONFIG_TASK_IO_ACCOUNTING
CONFIG_TASK_XACCT
CONFIG_TASK_DELAY_ACCT

If your kernel does not support I/O accounting, you may politely ask your kernel dev to enable it in his defconfig. But always remember, it's his call and you have to accept whatever he's gonna do. There is nothing you can do about it.


Usage
You can execute the script from wherever you like, be it your sdcard, data partition or system partition. But for easier use, I would recommend you to place it in your /system/bin folder.

(for this example, I assume you've placed it in /system/bin)
To run it, you must be root (---> $su )
Then you can run the actual script
Code:
iotop.sh

You don't like the units being KB? How about MB?
Code:
iotop.sh -m

Still not what you want? Bytes then?
Code:
iotop.sh -b

Found your desired unit? Great! But those entries with no I/O activity are quite annoying, right? So let's get rid of them!
Code:
iotop.sh --only

You don't want to see all those empty entries, but still want to know how many were skipped? No problem:
Code:
iotop-sh --only --show-skips

Still need some help? Check this:
Code:
iotop.sh --help
