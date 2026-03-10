#  Advanced settings

> [!WARNING]
> These settings are exclusive to ByeByeDPI! They are not compatible with ByeDPI arguments. Do not attempt to use strategies containing these settings in other software.
> Do not share strategies using these settings online, as their values depend heavily on your specific ByeByeDPI configuration.

> [!CAUTION]
> These settings are intended for advanced users. If you are unfamiliar with terms like Proxy Test, strategies, parameters, or flags, do not change anything. This page will not be helpful to you.

### SNI for fake packets
The Proxy Test includes a function to change the SNI for fake packets. It is set to google.com by default, but you can change it.

Changing this only makes sense if you have a well-thought-out bypass method and are certain that your ISP's filter checks packets against an SNI "whitelist."

[!CAUTION]
Do not change the SNI to a host from a blocked domain list (e.g., youtube.com or googlevideo.com). This will only signal to the filter that you are trying to access a blocked site.

Встроенные стратегии подхватывают SNI из настроек автоматически. Если вы хотите, чтобы ваша стратегия имела поддержку такой функции - вам стоит прописать у флага `-n` параметр `{sni}`, получиться должно так:

```
-n {sni}
```

Затем [передать](features.md/#my-list) уже изменённую стратегию в автоподбор.

### <a id="replace-proxy-lists">Замена списков для проксирования</a>

В byedpi есть фильтры для проксирования, которые принимают различные списки: `-H` и `-j`.

Чтобы передать в них списки доменов/подсетей, нужно вставить его по правилам byedpi, то есть примерно так:

```
-H:"domain1.com domain2.com domain3.com domain4.com domain5.com ..."
```
При большом списке доменов такой вариант может оказаться неудобным. ByeByeDPI (с версии 1.7.3) добавляет кастомный параметр `{list}`.

> [!TIP]
> Этот параметр работает и для автоподбора, и для командной строки, если вы примените такую стратегию - она перед отправкой в byedpi изменится на ту, которую последний сможет прочитать.

Чтобы его использовать, необходимо указать ID (название, например Cloudflare из встроенных) списка доменов/подсетей из [настроек автоподбора](features.md/#domain-list). Можно создать свой список и указать его название. Получиться должно примерно так:

```
-H:"{list:Cloudflare}"
```
или
```
-j:"{list:subnets}"
```
Второе будет работать ТОЛЬКО если у вас в разделе [настроек доменов](features.md/#domain-list) прописан список из подсетей с названием `subnets`.
