# autossh

Usage:

```python
from autossh import AutoSSHTunnel  

with AutoSSHTunnel(
    ssh_server='ssh.example.com', 
    ssh_username='your_username', 
    ssh_password='your_password', 
    remote_host='remote.example.com', 
    remote_port=3306, 
    local_port=5000,
    ssh_port=2222   
) as tunnel:
    info = tunnel.get_tunnel_info()
    print(f"SSH tunnel established from local port {info['local_port']} to {info['remote_host']}:{info['remote_port']}")
    print(f"Tunnel is active: {'Yes' if info['is_active'] else 'No'}")

```
Or: 

```python
from autossh import AutoSSHTunnel  

tunnel = AutoSSHTunnel(
    ssh_server='ssh.example.com', 
    ssh_username='your_username', 
    ssh_password='your_password', 
    remote_host='remote.example.com', 
    remote_port=3306, 
    local_port=5000,
    ssh_port=2222  
)

tunnel.start()

try:
    info = tunnel.get_tunnel_info()
    print(f"SSH tunnel established from local port {info['local_port']} to {info['remote_host']}:{info['remote_port']}")
    print(f"Tunnel is active: {'Yes' if info['is_active'] else 'No'}")
finally:
    tunnel.stop()
```

Or with cli:

```shell
autossh-py your_username@ssh.example.com -L 5000:remote.example.com:3306 -p 2222
```

If you want to use in backend, you can specify password with sshpass and use nohup &:

Install sshpass as per: https://gist.github.com/arunoda/7790979 and:

```shell
nohup sshpass -p your_password autossh-py -p 2222 -L 5000:remote.example.com:3306 your_username@ssh.example.com &
```

Also support ssh key:

```shell
autossh-py -i ~/your_key -L 3306:localhost:3306 your_username@ssh.example.com
```
