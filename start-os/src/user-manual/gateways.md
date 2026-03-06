# Gateways

A gateway is what connects your server to the Internet. There are two types of gateways: outbound only and inbound/outbound.

## Inbound/Outbound Gateways

An inbound/outbound gateway handles traffic in both directions — it routes outbound traffic _and_ accepts inbound connections from the Internet. Your router is an inbound/outbound gateway. StartTunnel is also an inbound/outbound gateway.

Think of the inbound side as a defense perimeter with hundreds of locked doors, each door leading to a unique service interface. For example, one door might say "Vaultwarden UI", another might say "Bitcoin RPC", and yet another might say "Bitcoin P2P".

If you want to let a specific person through a particular door, you give them a key. This is the equivalent of giving someone private VPN access to a specific service interface. If you want to let _everyone_ through a particular door, you remove the lock altogether. This is the equivalent of forwarding a port in your gateway, thereby exposing a particular service interface or domain to the public Internet.

> [!NOTE]
> If you are running StartOS on a VPS with a public IP address, there is no local network. Your gateway is inherently public and open to the Internet.

For guidance on choosing a gateway for clearnet hosting, see [Clearnet](public-access/clearnet.md#choosing-a-gateway).

## Outbound Only Gateways

An outbound only gateway (or outbound VPN) routes traffic _from_ your server to the Internet but does not accept inbound connections. A common example is a commercial VPN provider such as Mullvad or ProtonVPN. When you add a gateway to StartOS using a standard WireGuard configuration file, StartOS automatically detects it as an outbound only gateway.

You might want an outbound only gateway to hide your server's real IP address from external services, protect against your ISP monitoring or logging your traffic, or route sensitive services through a trusted VPN provider for added privacy.

## Adding a Gateway

1. Navigate to `System > Gateways` and click "Add".

1. Upload or paste the WireGuard configuration file from your VPN provider or StartTunnel instance.

   StartOS will automatically detect the gateway type:
   - **StartTunnel** config files are recognized and marked as _inbound-outbound_ gateways, capable of both receiving inbound connections and routing outbound traffic.
   - **All other** WireGuard configs (e.g. Mullvad, ProtonVPN, or any standard WireGuard provider) are marked as _outbound-only_ gateways.

## Outbound Traffic

By default, StartOS dynamically selects which gateway to use for outbound traffic for maximum performance. You can override this behavior using the select dropdown in the "Outbound Traffic" section underneath the "Gateways" table. This forces _all_ outbound traffic for everything on the server through the selected gateway.

### Per Service Overrides

You can further override this on a per-service basis by navigating to a service and going to **Actions > Set Outbound Gateway**. This is useful for routing sensitive services through a commercial VPN while leaving other services on the default.
