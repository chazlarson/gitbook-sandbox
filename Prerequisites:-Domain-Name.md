**You will need a domain name** as Cloudbox apps are only accessed via https://appname._yourdomain.com_ (see [[Basics: Accessing Cloudbox Apps]]). The steps below will help you set up a domain and DNS settings for use with Cloudbox.

Ports are [for the most part] bound only to the internal `cloudbox` docker network, which means they are not visible on the host; you won't be able to connect to the apps using `IP:PORT`.

# 1. Domain Provider

Get a domain name from any domain name registry (e.g. [Namecheap](https://Namecheap.com), [Godaddy](https://Godaddy.com), [Namesilo](https://Namesilo.com), etc).

If you already have one, you may skip this step.

_Note: Free domain name providers, such as [Freenom](https://www.freenom.com/), do not support wildcard DNS settings, and paid domain names can be had for less than a dollar per year (see promo deals on various sites). However, you can add them to [[Cloudflare|Prerequisites: Cloudflare]] and not have to worry about it._

If you are planning to use the automatic Cloudflare integration, there are some top-level domains [TLDs] that will not work with it.  Refer to [this page](https://support.cloudflare.com/hc/en-us/articles/360020296512-DNS-Troubleshooting-FAQ).

As of 2020/07/26:  "DNS API cannot be used for domains with .cf, .ga, .gq, .ml, or .tk TLDs."

# 2. DNS Setup

Pick one of the setups below. This will on whether you meet certain criteria, as listed under the "Notes" section.

## i. Wildcard DNS Setup

**Notes:**

 - For DNS providers that allow wildcards.

 - For [[Cloudbox install type|Basics: Cloudbox Install Types]].

**Steps:**


Created an A Record for your subdomains with `*` for host and set the value to your server IP address.

   | **Type** | **Host** | **Value**           | **TTL**   |
   |:-------- |:-------- |:------------------- |:--------- |
   | A Record | *        | _Server IP Address_ | 300       |


<details><summary>Example</summary>

Namecheap > Domain List > Manage > Advanced DNS > Add New Record > A Record > `*` for Host > Server IP for Value.

   ![](http://i.imgur.com/I7h5jSs.png)

</details>

## ii. Non-Wildcard DNS Setup

**Notes:**

 - For DNS providers that do not allow wildcards (e.g. Freenom).

 - For [[Mediabox / Feederbox  install types|Basics: Cloudbox Install Types]].

 - For [[Cloudflare|Prerequisites: Cloudflare]] users.

   Note: if you provide a Cloudflare email and API Key in your settings, the Cloudbox installer will set this up for you automatically.


### Cloudbox Install Type

You will need to create A Records for all Cloudbox subdomains. 


  | **Type** | **Host**     | **Value**               | **TTL**   |
  |:-------- |:------------ |:----------------------- |:--------- |
  | A Record | plex         | _Cloudbox IP Address_   | 300 |
  | A Record | plexpy       | _Cloudbox IP Address_   | 300 |
  | A Record | plexrequests | _Cloudbox IP Address_   | 300 |
  | A Record | jackett      | _Cloudbox IP Address_   | 300 |
  | A Record | radarr       | _Cloudbox IP Address_   | 300 |
  | A Record | sonarr       | _Cloudbox IP Address_   | 300 |
  | A Record | rutorrent    | _Cloudbox IP Address_   | 300 |
  | A Record | nzbget       | _Cloudbox IP Address_   | 300 |
  | A Record | nzbhydra2    | _Cloudbox IP Address_   | 300 |
  | A Record | organizr     | _Cloudbox IP Address_   | 300 |
  | A Record | portainer    | _Cloudbox IP Address_   | 300 |


### Mediabox / Feederbox Install Type

You will need to create A Records for both IP addresses (Media and Feeder boxes) and set them to their respective subdomains. 


#### Mediabox

  | **Type** | **Host**     | **Value**               | **TTL**   |
  |:-------- |:------------ |:----------------------- |:--------- |
  | A Record | plex         | _Mediabox IP Address_  | 300 |
  | A Record | plexpy       | _Mediabox IP Address_  | 300 |
  | A Record | plexrequests | _Mediabox IP Address_  | 300 |

#### Feederbox

  | **Type** | **Host**     | **Value**               | **TTL**   |
  |:-------- |:------------ |:----------------------- |:--------- |
  | A Record | jackett      | _Feederbox IP Address_ | 300 |
  | A Record | radarr       | _Feederbox IP Address_ | 300 |
  | A Record | sonarr       | _Feederbox IP Address_ | 300 |
  | A Record | rutorrent    | _Feederbox IP Address_ | 300 |
  | A Record | nzbget       | _Feederbox IP Address_ | 300 |
  | A Record | nzbhydra2    | _Feederbox IP Address_ | 300 | 
  | A Record | organizr     | _Feederbox IP Address_ | 300 |
  | A Record | portainer    | _Feederbox IP Address_ | 300 |



