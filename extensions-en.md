#  Advanced options

> [!WARNING]
> These settings are **exclusive to ByeByeDPI**! They are not compatible with ByeDPI arguments. Do not attempt to use strategies containing these settings in other software.
> **Do not share strategies using these settings**, as they're depended heavily on your specific ByeByeDPI configuration.

> [!CAUTION]
> These settings are intended for advanced users. If you are unfamiliar with terms like Proxy Test, strategies, byedpi options and flags, proceed at your own risk. This page will not be helpful to you.

### SNI for fake packets

The Proxy Test includes a option to change SNI for fake packets. It is set to `google.com` by default, but you can change it.

Changing this only makes sense if you have a well-thought-out bypass method and are certain that your ISP's filter checks packets against an SNI "whitelist".

[!CAUTION]
> Do not change the SNI to a host from a blocked domain list (youtube.com or googlevideo.com (in Russia)). This will let the filter know that you are trying to access a blocked site.

Built-in strategies are auto taking SNI from settings. If you want for your strategy to be able to support this function - you need to specify the setting for `-n` flag a special parameter `{sni}`, so it'll be like this:

```
-n {sni}
```

And then [pass](features.md/#my-list) your modified strategy to Proxy Test.

### <a id="replace-proxy-lists">Replace lists for routing</a>

ByeDPI has routing filters that accept different lists: `-H` and `-j`.

To use them correctly, you need to pass them a list of domains or IP-addresses, as specified in byedpi:

```
-H:"domain1.com domain2.com domain3.com domain4.com domain5.com ..."
```
For large domain sets this option may seem as uncomfortable. ByeByeDPI (from version 1.7.3) implements a custom option `{list}`.

> [!TIP]
> This option works for Proxy Test and for command line settings. If you apply a strategy with this option, ByeByeDPI will change it to a readible for byedpi variant.

To use this feature you need to specify an ID (it is represented as name, for example: Cloudflare from built-in) of list from [Proxy Test settings](features-en.md/#domain-list). You can also make a custom list and set its name. It should be as follows:

```
-H:"{list:Cloudflare}"
```
or

```
-j:"{list:subnets}"
```
The second will work ONLY if a list with name `subnets` exists in [domains settings](features-en.md/#domain-list) page.
