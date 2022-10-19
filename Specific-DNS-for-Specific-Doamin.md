
# Using different DNS servers for different domains

## Windows:
The Add-DnsClientNrptRule cmdlet adds a Name Resolution Policy Table (NRPT) rule for the specified namespace.

Run the following command as Administrator
    
```bash
Add-DnsClientNrptRule -Namespace "your.domain.name" -NameServers "10.0.0.1"  # IP with DNS IP 
```
## Linux:

```bash
$ sudo nano /etc/systemd/resolved.conf
```   
Add following lines at the end of file 

```bash        
[Resolve]
DNS=10.0.0.1 10.0.0.2 # Change the IP according to you DNS1 DNS2 
Domains=your.domain.name # Chane it witth youur domain name
```
## Mac:
To add an additional resolver to a Mac, create a directory at `/etc/resolver`.
```bash
$ sudo mkdir /etc/resolver
```
For each domain that you want to hit a specific nameserver, create a file with the name of your desired domain and a nameserver line (or lines) in the file. For my internal domain I used the following command:

```bash
$ cat 'nameserver 192.168.1.1' > /etc/resolver/your.domain.name # Change the IP witth your DNS IP and file name with you domain name
```    
