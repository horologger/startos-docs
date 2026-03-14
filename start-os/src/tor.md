# Tor

Access your server over the Tor network using `.onion` addresses. Tor provides anonymous, censorship-resistant connections and requires installing the Tor service from the StartOS marketplace. Onion addresses can be kept private or published for public hosting.

## Use Case

Tor lets you host services on the overlay network as `.onion` domains. How you use an onion address determines whether it functions as private or public access:

1. **Private and anonymous**. Unless you share or leak a Tor address, nobody knows it exists and nobody knows it belongs to you. It is your secure, secret tunnel to the underlying website/API.

1. **Public and anonymous**. If you publish a Tor address _without_ associating it with your identity (not easy to do), people know it exists but nobody knows it belongs to you. By this method, you can anonymously host a censorship-resistant website/API on the private web.

1. **Public and identified**. If you publish a Tor address _and_ associate it with your identity, people know it exists and they know it belongs to you. This is useful for hosting an identified yet still censorship-resistant website/API, or for sharing access with friends and family.

> [!WARNING]
> It is normal for Tor connections to be slow or unreliable at times.

## Setting Up Tor

Tor is not included in StartOS by default. To use Tor, you must install the **Tor** service from the marketplace.

1. Go to the Marketplace and install the **Tor** service.

1. Start the Tor service and wait for it to become healthy.

## Managing Onion Services

Once Tor is installed and running, you can create `.onion` addresses for specific service interfaces on your server.

1. Open the Tor service and go to **Actions > Manage Onion Services**.

1. Select a service interface to create an onion address for.

1. To view your onion addresses, go to **Actions > View Onion Addresses**.

> [!TIP]
> When creating an onion service, you can upload a private key to use a vanity address. For instructions on generating a vanity address, see [here](https://community.torproject.org/onion-services/advanced/vanity-addresses/).

> [!NOTE]
> Each onion domain produces two addresses: `HTTP` and `HTTPS`. Because Tor is a secure protocol, it is perfectly safe to use the `HTTP` address. It is also preferable, because it does not require anyone to trust your server's Root CA. Some applications may require `HTTPS`, in which case the certificate is signed by your server's Root CA.

## Connecting over Tor

### Using a Tor Browser

You can connect to your server and installed services from anywhere in the world, privately and anonymously, by visiting their unique `http://....onion` URLs from any Tor-enabled browser.

> [!TIP]
> Recommended Browsers
>
> - Mac, Linux, Windows, Android/Graphene: [Tor Browser](https://torproject.org/download)
> - iOS: [Onion Browser](https://onionbrowser.com)

### Running Tor in the _Background_ on your Phone/Laptop

By running Tor in the background on your phone or laptop, certain apps can connect over Tor, even if the apps themselves do not natively support Tor.

For instructions specific to your device's operating system, use a search engine or AI. This capability is well documented.

## Public Hosting

Onion addresses can also serve as a public hosting method. Unlike clearnet domains, onion addresses do not require purchasing a domain, configuring DNS, or opening ports. Anyone with a Tor-enabled browser can reach them.

- **Censorship resistance**. Onion services cannot be taken down by domain registrars, DNS providers, or ISPs. As long as your server is running, the address is reachable.

- **Anonymity** (if done carefully). If you publish an onion address without associating it with your identity, observers can access your service but cannot determine who operates it. Achieving true anonymity requires careful operational security — for example, never linking the address to your real identity, and not leaking metadata that could be correlated.

- **No infrastructure dependencies**. You do not need a static IP, a domain name, or port forwarding. Tor handles routing entirely through its overlay network.

The difference between private and public Tor access is simply in how you use the addresses: keeping them secret vs. sharing them publicly.
