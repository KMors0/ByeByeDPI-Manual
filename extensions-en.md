#  Advanced options

> [!WARNING]
> These settings are **exclusive to ByeByeDPI**! They are not compatible with ByeDPI arguments. Do not attempt to use strategies containing these settings in other software.
> **Do not share strategies using these settings to Internet**, as their values depend heavily on your specific ByeByeDPI configuration.

> [!CAUTION]
> These settings are intended for advanced users. If you are unfamiliar with terms like Proxy Test, strategies, options, or flags, do not change anything. This page will not be helpful to you.

### SNI for fake packets
The Proxy Test includes a function to change the SNI for fake packets. It is set to google.com by default, but you can change it.

Changing this only makes sense if you have a well-thought-out bypass method and are certain that your ISP's filter checks packets against an SNI "whitelist."

[!CAUTION]
> Do not change the SNI to a host from a blocked domain list (youtube.com or googlevideo.com (in Russia)). This will only signal to the filter that you are trying to access a blocked site.

Built-in strategies auto taking SNI from settings. If you want to strategy support this function - you need specify the setting for `-n` flag parameter `{sni}`. Example:

```
-n {sni}
```

After [transfer](features.md/#my-list) modified strategy to Proxy Test.

### <a id="replace-proxy-lists">Replace lists for proxy</a>

In ByeDPI there is filters for proxy, that accept different lists: `-H` and `-j`.

For replace domains/IP to lists need paste by ByeDPI rules. Example:

```
-H:"domain1.com domain2.com domain3.com domain4.com domain5.com ..."
```
For big lists this option may seem is uncomfortable. ByeByeDPI (from version 1.7.3) have a custom option `{list}`.

> [!TIP]
> This option working and for Proxy Test and for command line. If you apply like these strategy - before sent to ByeDPI strategy changing to readable variation.

For using this feature need specify ID (name of list, example: Cloudflare from built-in) list of domains/IP from [Proxy Test settings](features-en.md/#domain-list). You can make a custom list and set name. Example:

```
-H:"{list:Cloudflare}"
```
or

```
-j:"{list:subnets}"
```
Two working ONLY if in [domains settings](features-en.md/#domain-list) page there list with name `subnets`.
