# Network Traffic Analysis Lab

## Objective

Use Wireshark to inspect packet headers, identify protocols and communication direction, and document observations from a small controlled exchange.

## Environment and scope

- Analyzer and traffic source: Kali Linux, Wireshark 4.6.6
- Peer: Metasploitable 2, an intentionally vulnerable Linux VM
- Network: VirtualBox host-only network
- Kali address: `192.168.56.103`
- Target address: `192.168.56.102`
- Scope: traffic intentionally generated between these two lab VMs

## Exercises and observations

### ARP and ICMP

Generated four ping requests from Kali to Metasploitable with `ping -c 4 192.168.56.102`. The capture displayed four ICMP Echo requests and four Echo replies, plus four ARP packets used to resolve local IPv4 addresses to link-layer addresses. Wireshark displayed 12 packets total and zero dropped packets. An inspected request was 98 bytes on the wire, with a 40-byte ICMP data field.

### HTTP

Requested the target's home page with `curl http://192.168.56.102/`. Wireshark displayed a `GET / HTTP/1.1` request from Kali and an `HTTP/1.1 200 OK` response from the target. The response was HTML and exposed server identification headers, including Apache 2.2.8 and PHP 5.2.4. The inspected response packet was 1,133 bytes.

## Defensive observations

- HTTP content and headers were readable in this lab capture because the request used unencrypted HTTP. Use HTTPS for applications handling sensitive data.
- Server/version details appeared in the response. Keep web software supported and patched, and avoid unnecessary version disclosure.
- ARP and ICMP were expected for local address resolution and connectivity testing. Their presence alone is not suspicious; interpret packets in context.
- Keep intentionally vulnerable training VMs isolated from untrusted and production networks.

## Limitations

The capture covers only a short ping exchange and a single HTTP page request between lab VMs. It does not represent all target traffic, establish malicious activity, or prove a vulnerability. No credentials or sensitive data were used. The PCAPNG file remains in the Kali VM and was not transferred into this repository.

## Reproduction

Start a Wireshark capture on Kali's host-only interface (`eth0` in this setup), then generate the traffic:

```bash
ping -c 4 192.168.56.102
curl http://192.168.56.102/
```

Use the `icmp` and `http` display filters to inspect the respective traffic, then save the capture as PCAPNG. Capture only traffic you own or are authorized to analyze.