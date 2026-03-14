# Private Access

Private access means connecting to your server and its services without exposing anything to the public Internet. Only you and your authorized devices can reach your server. StartOS supports several private access strategies, each with different tradeoffs.

## When to Use Private Access

Most people will use private access for most of their services most of the time. Unless you are intentionally hosting something for the public (a website, a blog, a Lightning node), your services should be privately accessible only to you and your trusted devices.

## Strategies

- **[LAN](lan.md)** — The fastest option. Traffic stays on your local network and never reaches the Internet. Requires being connected to the same network as your server and [trusting your Root CA](trust-ca.md).

- **[VPN](inbound-vpn.md)** — Extends your local network to anywhere in the world. Authorized devices get a secure tunnel to your server as if they were on the same LAN. Requires either a router with VPN server capability or [StartTunnel](/start-tunnel/), and [trusting your Root CA](trust-ca.md).

- **[Tor](tor.md)** — Anonymous, censorship-resistant access using `.onion` addresses. Works from anywhere without any router configuration or Root CA trust. Connections are slower and occasionally unreliable. Requires installing the **Tor** service from the marketplace.

- **[Holesail](holesail.md)** — Direct peer-to-peer encrypted tunnels with no port forwarding, static IPs, or Root CA trust required. Once connected, traffic flows directly between peers, so speeds are comparable to VPN. Works behind restrictive networks. Requires installing the **Holesail** service from the marketplace.

## Combining Strategies

These strategies are not mutually exclusive. A common setup is:

- **LAN** for daily use at home
- **VPN** or **Holesail** for remote access from your own devices
- **Tor** for access from untrusted networks or when anonymity matters
