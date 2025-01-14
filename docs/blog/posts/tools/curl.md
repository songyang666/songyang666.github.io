---
date:
  created: 2025-01-14
  updated: 2025-01-14
categories:
  - curl
readtime: 1
authors:
  - charlie
---
# curl
#  curl 手册
```bash
man curl
```
## curl 30X redirect handle

关于处理30x 加上如下参数
```text
  -L, --location
              (HTTP) If the server reports that the requested page has moved to a different location (indicated with a Location: header and a 3XX response code), this option makes curl redo the request on the new place. If used together with -i, --include or -I,
              --head, headers from all requested pages are shown.

              When authentication is used, curl only sends its credentials to the initial host. If a redirect takes curl to a different host, it does not get the user+password pass on. See also --location-trusted on how to change this.

              Limit the amount of redirects to follow by using the --max-redirs option.

              When curl follows a redirect and if the request is a POST, it sends the following request with a GET if the HTTP response was 301, 302, or 303. If the response code was any other 3xx code, curl resends the following request using the same unmodified
              method.

              You can tell curl to not change POST requests to GET after a 30x response by using the dedicated options for that: --post301, --post302 and --post303.

              The method set with -X, --request overrides the method curl would otherwise select to use.

              Providing --location multiple times has no extra effect.  Disable it again with --no-location.

              Example:
               curl -L https://example.com

              See also --resolve and --alt-svc.


```
如果遇到Authorization没有带入到redirect 地址,如下参数
```text
  --location-trusted
              (HTTP) Like -L, --location, but allows sending the name + password to all hosts that the site may redirect to. This may or may not introduce a security breach if the site redirects you to a site to which you send your authentication info (which is
              clear-text in the case of HTTP Basic authentication).

              Providing --location-trusted multiple times has no extra effect.  Disable it again with --no-location-trusted.

              Example:
               curl --location-trusted -u user:password https://example.com

              See also -u, --user.

```
