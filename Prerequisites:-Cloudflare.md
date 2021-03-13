
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Intro](#intro)
- [Sign Up](#sign-up)
- [Setup](#setup)
- [Cloudflare API Key](#cloudflare-api-key)
- [Post-Setup](#post-setup)

<!-- /TOC -->

## Intro

[Cloudflare](https://www.cloudflare.com) a service that, among other things, protects and accelerates a wide network of websites. By being the "man in the middle", it can act like a free DNS provider.

Cloudbox makes adding subdomains to Cloudflare's DNS settings a breeze via automation. All you need is the API key.

Note that there are some top-level domains [TLDs] that will not work with this automation. Refer to [this page](https://support.cloudflare.com/hc/en-us/articles/360020296512-DNS-Troubleshooting-FAQ).

As of 2020/07/26: "DNS API cannot be used for domains with .cf, .ga, .gq, .ml, or .tk TLDs."

Although Cloudflare is not required for Cloudbox, it is still recommended because:

1. DNS changes propagate almost instantly (a lot faster than a domain provider's DNS service).

1. Hide your server's IP behind Cloudflare's.

1. Makes setting up Mediabox / Feederbox a lot quicker.

1. Allows for automated setup of subdomains for Cloudbox add-on apps.

1. Can optionally enable CDN / Proxy for your subdomains.

1. It's free.

_Note: Cloudbox does not enable CDN / Proxy by default, but you may do so yourself after installing Cloudbox (see section [[below|Prerequisites: Cloudflare#post-setup]])._



## Sign Up

1. Sign up for a free [Cloudflare](https://www.cloudflare.com/) account.

1. On your Domain Registrar's website (e.g. GoDaddy, Namecheap, etc), set the Name Servers to what Cloudflare instructs you to.

   - Examples:

     - Namecheap.com -> "Dashboard" -> _your domain.ltd_ -> "Manage" -> "Name Servers" -> "Custom DNS" -> add the nameservers in.

       ![](https://i.imgur.com/K4OI1XD.png)

     - Namesilo.com -> "Manage My Domains" -> _your domain.ltd_ -> "NameServers" -> "Change" ->  add the nameservers in.

       ![](https://i.imgur.com/a7DMp0I.png)

## Setup

1. Go to [Cloudflare.com](https://www.cloudflare.com/).

1. Here you will see that your domain will have an "Active" status. Click on your domain to continue.

   ![](https://i.imgur.com/p1hAy3a.png)

1. Click the **SSL/TLS** tab.

1. Set **SSL** to `Full (strict)`.

   ![](https://i.imgur.com/dyxN3UG.png)

<!-- Temporarily commented out - may not be needed..

1. Set **Always Use HTTPS** to `off`.

1. Set **HTTP Strict Transport Security (HSTS)** to `disabled`.

   ![](https://i.imgur.com/MaqAv5i.png)

-->

## Cloudflare API Key

1. Go to [Cloudflare.com](https://www.cloudflare.com/).

1. Click the **Overview** tab.

1. Click **Get your API token**.

   ![](https://i.imgur.com/O4eUa3G.png)

1. Under **API Keys** and then **Global API Key** click **View**.

   ![](https://i.imgur.com/quzUeop.png)

1. On the login popup, type in your **password** and click **View**.

   ![](https://i.imgur.com/gTLXDH2.png)

1. Save your API key.

   ![](https://i.imgur.com/ET91JKG.png)

## Post-Setup

After Cloudbox has added in the subdomains, you may go back in and turn on CDN for for them if you like.

But do this AFTER all your certs have been assigned and you have confirmed that all the Cloudbox app sites are loading OK. 

This also applies to any app/subdomains you add in the future - wait till after you get certs before enabling CDN.

_Note 1: Performance of your server may vary when CDN is enabled._

_Note 2: Leave the subdomains `cloudbox`, `mediabox`, and `feederbox` as `DNS Only`, as they were created to reach your servers directly and not behind a CDN proxy (i.e. they need to resolve to the server's IP and not Cloudflare's)._

You can do this by:

1. Going to [Cloudflare.com](https://www.cloudflare.com/).

1. Clicking the **DNS** tab.

1. Find the subdomain of interest.

1. Under "Status", click the gray cloud icon (i.e. `DNS Only`) to switch to an orange one (i.e. `DNS and HTTP proxy (CDN)`).

   ![](https://i.imgur.com/vKlKOSL.png)

If you do this to Plex/Emby subdomains, it is recommended that you disable caching or else you may be banned by Cloudflare for violating their TOS.

1. Going to [Cloudflare.com](https://www.cloudflare.com/).

1. Click the **Page Rules** tab.

1. Click the **Create a Page Rule** button. 

1. Create a rule for the relevant subdomain. 

   - If the URL matches: `subdomain.yourdomain.com/*`

   - Then the settings are:

     - Cache Level: `Bypass`

     - Disable Performance

   ![](https://i.imgur.com/Q430Lkz.png)

1. Click the **Save and Deploy** button.

   ![](https://i.imgur.com/plWElkf.png)

