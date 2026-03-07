# DNS

StartOS runs its own DNS server to resolve private domains for services on your server. This page covers how DNS works on StartOS and when you might need to change it.

## How It Works

By default, StartOS obtains its DNS servers from your router via [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol). For most users, the default settings require no changes. When you add a [private domain](private-access/lan.md#private-domains), StartOS automatically creates a DNS record on its internal DNS server.

For private domains to work, the gateway they are assigned to must use StartOS for DNS. StartOS will test this automatically and guide you through the setup if needed. The details depend on your gateway type:

- **Router**: Set StartOS as your router's primary DNS server. All routers support this feature. Refer to your router's user manual for detailed instructions.

  > [!WARNING]
  > It is possible that StartOS is already using your router for DNS. In this case, you cannot instruct your router to use StartOS for DNS, as this would be circular. If StartOS detects a potential circular DNS situation, it will warn you. To resolve this, switch to [static DNS servers](#static-dns-servers) so StartOS no longer relies on your router.

- **StartTunnel**: SSH into your StartTunnel VPS and run the following command:

      start-tunnel dns defer

> [!TIP]
> If your private domain is a real domain that you control, you can alternatively configure its DNS record at your registrar to resolve to your server's _LAN IP address_. In this case, the StartOS DNS server is not needed.

## Static DNS Servers

To view or change the DNS servers StartOS uses, navigate to `System > DNS`. To override the defaults, select "Static" and provide up to three DNS servers in order of preference.

> [!NOTE]
> If you want to use a specific DNS provider (such as Cloudflare or Quad9), it is generally better to configure it in your router so that all devices on your network benefit, not just your server.
