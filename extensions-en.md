#  Advanced settings

> [!WARNING]
> This settings is **exclusive** for ByeByeDPI! This isn't arguments for ByeDPI. Don't try using strategy with this settings in another software.
> Should not be shared strategy with this settings on Network, since their value **very** depends by ByeByeDPI settings.

> [!CAUTION]
> This settings for users with knowledge instrument. If you dont know, what is Proxy Test, strategy, parameters, flags, etc... — should not clicking all. This page don't help you.

### SNI fake packets

In proxy test since there function for change SNI on fake packets. By default set `google.com`, but you can change his.

Changing his make sense if you thought it through by-pass
methodимеет смысл в случае, если вы правильно продумали метод обхода блокировки и уверены, что ваш фильтр проверяет пакеты на предмет SNI из "Белого списка".

> [!CAUTION]
> Не следует менять SNI на хост из списка заблокированных (например, youtube.com или googlevideo.com) - это лишь даст фильтру понять, что вы ТОЧНО собираетесь сходить за чем-то заблокированным.

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
