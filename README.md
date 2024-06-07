This Python script allows you to scan ports on a remote host to check for open connections. Simply input the hostname or IP address of the remote host, along with the range of ports to scan, and the script will conduct the port scan. It utilizes the `socket` module for network communication and provides a simple yet effective way to perform port scanning tasks. This tool can be useful for network administrators, security professionals, and anyone interested in understanding the network security posture of a target system.

```python
import socket

def scan_ports(host, start_port, end_port):
    open_ports = []
    for port in range(start_port, end_port + 1):
        try:
            with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
                s.settimeout(1)
                s.connect((host, port))
            open_ports.append(port)
        except:
            pass
    return open_ports

def main():
    host = input("Enter the host to scan: ")
    start_port = int(input("Enter the starting port: "))
    end_port = int(input("Enter the ending port: "))

    print("Scanning ports...")
    open_ports = scan_ports(host, start_port, end_port)

    if open_ports:
        print("Open ports:")
        for port in open_ports:
            print(port)
    else:
        print("No open ports found.")

if __name__ == "__main__":
    main()
```
