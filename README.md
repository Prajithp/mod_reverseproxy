mod_reverseproxy
================

mod_reverseproxy - reverse proxy module for Apache

Based on mod_remoteip.c and mod_cloudflare.c , this Apache module  will replace the  remote_ip  variable in user's logs with the correct remote IP sent from frontend web server like nginx and varnish.

To install, follow the instructions on:
   ```bash
   https://raw.github.com/Prajithp/mod_reverseproxy/master/mod_reverseproxy.c
   apxs -i -a -c mod_reverseproxy.c  
   ```
## Configuration Directives ##
```bash
ReverseProxyRemoteIPHeader   X-Real-IP         - The header to use for the real IP
                                                 address.
ReverseProxyRemoteIPTrusted  127.0.0.1         -  What IPs to adjust requests for
```

## Example Configuration ##
```bash

LoadModule reverseproxy_module modules/mod_reverseproxy.so

<IfModule reverseproxy_module>
ReverseProxyRemoteIPHeader X-Real-IP
ReverseProxyRemoteIPTrusted 127.0.0.1
ReverseProxyRemoteIPTrusted 46.105.160.192
</IfModule>

```


NOTES:

- If mod\_cloudflare or mod\_remoteip are already  enabled on the same web server, the server will crash if they both try to set the remote IP to a different value.
