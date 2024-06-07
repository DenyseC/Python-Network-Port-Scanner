# Python-Network-Port-Scanner
Scan remote hosts for open ports from 1-1024. Quickly identify network vulnerabilities. Uses Python's socket module.


'''import asyncio

async def scan_port(host, port, results):
    try:
        reader, writer = await asyncio.open_connection(host, port)
        results[port] = "Open"
        writer.close()
    except (ConnectionRefusedError, OSError):
        results[port] = "Closed"

async def scan_ports(host, start_port, end_port):
    results = {}
    tasks = []
    for port in range(start_port, end_port + 1):
        tasks.append(scan_port(host, port, results))
    await asyncio.gather(*tasks)
    return results

async def main():
    host = input("Enter the host to scan: ")
    start_port = int(input("Enter the starting port: "))
    end_port = int(input("Enter the ending port: "))

    start_time = asyncio.get_event_loop().time()
    results = await scan_ports(host, start_port, end_port)
    end_time = asyncio.get_event_loop().time()

    for port, status in results.items():
        print(f"Port {port}: {status}")

    print(f"Scanning completed in {end_time - start_time:.2f} seconds.")

if __name__ == "__main__":'''
    asyncio.run(main())
