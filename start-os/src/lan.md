# LAN

Connect to your server over your local network using its [mDNS address](mdns.md) or direct IP address. This is the fastest connection method, as traffic stays on your LAN and never reaches the Internet.

## Use Case

Local connections are the fastest possible, as they do not reach out to the Internet. You must be connected to the same Local Area Network (LAN) as your server.

## Watch the Video

<div class="yt-video" data-id="lAMI43MC7fQ" data-title="Connecting Locally"></div>

## Option 1: mDNS Address

Your server's [mDNS address](mdns.md) (e.g. `my-cool-server.local`) is derived from your [server name](server-name.md) and resolves to your server's LAN IP address automatically.

## Option 2: IP Address

Your router automatically assigns your server an IP address on the LAN. The address can be found (1) in your StartOS dashboard at `System -> StartOS UI`, (2) in your router dashboard, or (3) by `pinging` your server's mDNS address from the command line of a computer on the same network.

> [!IMPORTANT]
> Your router may unexpectedly change your server's IP address on the LAN. To avoid this, we _highly_ recommend assigning a static IP address. This becomes _necessary_ if you intend to access your server via VPN or clearnet. All routers support setting a static IP address for devices on the LAN. Refer to your router's user manual for detailed instructions.

## Private Domains

You can also assign [private domains](private-domains.md) to service interfaces. Private domains work like the mDNS address but also work over [VPN](inbound-vpn.md) and can be anything you choose.
