#CHANGE LOG Apache HTTP Server

27-Januari-2017 Changes with Apache 2.4.25 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.2k from 1.0.2j (Changelog)

*) Upgraded pcre to 8.40 from 8.39 (Changelog)

*) Upgraded zlib to 1.2.11 from 1.2.8 (Changelog)

ASF changes:

*) mod_proxy_{ajp,fcgi}: Fix a possible crash when reusing an established backend connection, happening with LogLevel trace2 or higher configured, or at any log level with compilers not detected as C99 compliant (e.g. MSVC on Windows). [Yann Ylavic]

19-December-2016 Changes with Apache 2.4.25 ASF changes:

*) Fix some build issues related to various modules. [Rainer Jung] 16-December-2016 Changes with Apache 2.4.24 (not released) Apache Lounge changes:

*) Upgraded nghttp2 to 1.17.0 from 1.12.0 (Changelog)

ASF changes:

*) SECURITY: CVE-2016-8740 (cve.mitre.org) mod_http2: Mitigate DoS memory exhaustion via endless CONTINUATION frames. [Naveen Tiwari < naveen.tiwari@asu.edu > and CDF/SEFCOM at Arizona State University, Stefan Eissing]

*) SECURITY: CVE-2016-5387 (cve.mitre.org) core: Mitigate [f]cgi "httpoxy" issues. [Dominic Scheirlinck < dominic vendhq.com >, Yann Ylavic]

*) SECURITY: CVE-2016-2161 (cve.mitre.org) mod_auth_digest: Prevent segfaults during client entry allocation when the shared memory space is exhausted. [Maksim Malyutin < m.malyutin dsec.ru >, Eric Covener, Jacob Champion]

*) SECURITY: CVE-2016-0736 (cve.mitre.org) mod_session_crypto: Authenticate the session data/cookie with a MAC (SipHash) to prevent deciphering or tampering with a padding oracle attack. [Yann Ylavic, Colm MacCarthaigh]

*) SECURITY: CVE-2016-8743 (cve.mitre.org) Enforce HTTP request grammar corresponding to RFC7230 for request lines and request headers, to prevent response splitting and cache pollution by malicious clients or downstream proxies. [William Rowe, Stefan Fritsch]

*) Validate HTTP response header grammar defined by RFC7230, resulting in a 500 error in the event that invalid response header contents are detected when serving the response, to avoid response splitting and cache pollution by malicious clients, upstream servers or faulty modules. [Stefan Fritsch, Eric Covener, Yann Ylavic]

*) mod_rewrite: Limit runaway memory use by short circuiting some kinds of looping RewriteRules when the local path significantly exceeds LimitRequestLine. PR 60478. [Jeff Wheelhouse < apache wheelhouse.org >]

*) mod_ratelimit: Allow for initial "burst" amount at full speed before throttling: PR 60145 [Andy Valencia < ajv-etradanalhos vsta.org >, Jim Jagielski]

*) mod_socache_memcache: Provide memcache stats to mod_status. [Jim Jagielski]

*) http_filters: Fix potential looping in new check_headers() due to new pattern of ap_die() from http header filter. Explicitly clear the previous headers and body.

*) core: Drop Content-Length header and message-body from HTTP 204 responses. PR 51350 [Luca Toscano]

*) mod_proxy: Honor a server scoped ProxyPass exception when ProxyPass is configured in < Location >, like in 2.2. PR 60458. [Eric Covener]

*) mod_lua: Fix default value of LuaInherit directive. It should be 'parent-first' instead of 'none', as per documentation. PR 60419 [Christophe Jaillet]

*) core: New directive HttpProtocolOptions to control httpd enforcement of various RFC7230 requirements. [Stefan Fritsch, William Rowe]

*) core: Permit unencoded ';' characters to appear in proxy requests and Location: response headers. Corresponds to modern browser behavior. [William Rowe]

*) core: ap_rgetline_core now pulls from r->proto_input_filters.

*) core: Correctly parse an IPv6 literal host specification in an absolute URL in the request line. [Stefan Fritsch]

*) core: New directive RegisterHttpMethod for registering non-standard HTTP methods. [Stefan Fritsch]

*) mod_socache_memcache: Pass expiration time through to memcached. [Faidon Liambotis < paravoid debian.org >, Joe Orton]

*) mod_cache: Use the actual URI path and query-string for identifying the cached entity (key), such that rewrites are taken into account when running afterwards (CacheQuickHandler off). PR 21935. [Yann Ylavic]

*) mod_http2: new directive 'H2EarlyHints' to enable sending of HTTP status 103 interim responses. Disabled by default. [Stefan Eissing]

*) mod_ssl: Fix quick renegotiation (OptRenegotiaton) with no intermediate in the client certificate chain. PR 55786. [Yann Ylavic]

*) event: Allow to use the whole allocated scoreboard (up to ServerLimit slots) to avoid scoreboard full errors when some processes are finishing gracefully. Also, make gracefully finishing processes close all keep-alive connections. PR 53555. [Stefan Fritsch]

*) mpm_event: Don't take over scoreboard slots from gracefully finishing threads. [Stefan Fritsch]

*) mpm_event: Free memory earlier when shutting down processes. [Stefan Fritsch]

*) mod_status: Display the process slot number in the async connection overview. [Stefan Fritsch]

*) mod_dir: Responses that go through "FallbackResource" might appear to hang due to unterminated chunked encoding. PR58292. [Eric Covener]

*) mod_dav: Fix a potential cause of unbounded memory usage or incorrect behavior in a routine that sends < DAV:response >'s to the output filters. [Evgeny Kotkov]

*) mod_http2: new directive 'H2PushResource' to enable early pushes before processing of the main request starts. Resources are announced to the client in Link headers on a 103 early hint response. All responses with status code <400 are inspected for Link header and trigger pushes accordingly. 304 still does prevent pushes. 'H2PushResource' can mark resources as 'critical' which gives them higher priority than the main resource. This leads to preferred scheduling for processing and, when content is available, will send it first. 'critical' is also recognized on Link headers. [Stefan Eissing]

*) mod_proxy_http2: uris in Link headers are now mapped back to a suitable local url when available. Relative uris with an absolute path are mapped as well. This makes reverse proxy mapping available for resources announced in this header. With 103 interim responses being forwarded to the main client connection, this effectively allows early pushing of resources by a reverse proxied backend server. [Stefan Eissing]

*) mod_proxy_http2: adding support for newly proposed 103 status code. [Stefan Eissing]

*) mpm_unix: Apache fails to start if previously crashed then restarted with the same PID (e.g. in container). PR 60261. [Val < valentin.bremond gmail.com >, Yann Ylavic]

*) mod_http2: unannounced and multiple interim responses (status code < 200) are parsed and forwarded to client until a final response arrives. [Stefan Eissing]

*) mod_proxy_http2: improved robustness when main connection is closed early by resetting all ongoing streams against the backend. [Stefan Eissing]

*) mod_http2: allocators from slave connections are released earlier, resulting in less overall memory use on busy, long lived connections. [Stefan Eissing]

*) mod_remoteip: Pick up where we left off during a subrequest rather than running with the modified XFF but original TCP address. PR 49839/PR 60251

*) http: Respond with "408 Request Timeout" when a timeout occurs while reading the request body. [Yann Ylavic]

*) mod_http2: connection shutdown revisited: corrected edge cases on shutting down ongoing streams, changed log warnings to be less noisy when waiting on long running tasks. [Stefan Eissing]

*) mod_http2: changed all AP_DEBUG_ASSERT to ap_assert to have them available also in normal deployments. [Stefan Eissing]

*) mod_http2/mod_proxy_http2: 100-continue handling now properly implemented up to the backend. Reused HTTP/2 proxy connections with more than a second not used will block request bodies until a PING answer is received. Requests headers are not delayed by this, since they are repeatable in case of failure. This greatly increases robustness, especially with busy server and/or low keepalive connections. [Stefan Eissing]

*) mod_proxy_http2: fixed duplicate symbols with mod_http2. [Stefan Eissing]

*) mod_http2: rewrite of how responses and trailers are transferred between master and slave connection. Reduction of internal states for tasks and streams, stability. Heuristic id generation for slave connections to better keep promise of connection ids unique at given point int time. Fix for mod_cgid interop in high load situtations. Fix for handling of incoming trailers when no request body is sent. [Stefan Eissing]

*) mod_http2: fix suspended handling for streams. Output could become blocked in rare cases. [Stefan Eissing]

*) mpm_winnt: Prevent a denial of service when the 'data' AcceptFilter is in use by replacing it with the 'connect' filter. PR 59970. [Jacob Champion]

*) mod_cgid: Resolve a case where a short CGI response causes a subsequent CGI to be killed prematurely, resulting in a truncated subsequent response. [Eric Covener]

*) mod_proxy_hcheck: Set health check URI and expression correctly for health check worker. PR 60038 [zdeno < zdeno scnet.sk >]

*) mod_http2: if configured with nghttp2 1.14.0 and onward, invalid request headers will immediately reset the stream with a PROTOCOL error. Feature logged by module on startup as 'INVHD' in info message. [Stefan Eissing]

*) mod_http2: fixed handling of stream buffers during shutdown. [Stefan Eissing]

*) mod_reqtimeout: Fix body timeout disabling for CONNECT requests to avoid triggering mod_proxy_connect's AH01018 once the tunnel is established. [Yann Ylavic]

*) ab: Set the Server Name Indication (SNI) extension on outgoing TLS connections (unless -I is specified), according to the Host header (if any) or the requested URL's hostname otherwise. [Yann Ylavic]

*) mod_proxy_fcgi: avoid loops when ProxyErrorOverride is enabled and the error documents are proxied. PR 55415. [Luca Toscano]

*) mod_proxy_fcgi: read the whole FCGI response even when the content has not been modified (HTTP 304) or in case of a precondition failure (HTTP 412) to avoid subsequent bogus reads and confusing error messages logged. [Luca Toscano]

*) mod_http2: h2 status resource follows latest draft, see http://www.ietf.org/id/draft-benfield-http2-debug-state-01.txt [Stefan Eissing]

*) mod_http2: handling graceful shutdown gracefully, e.g. handling existing streams to the end. [Stefan Eissing]

*) mod_proxy_{http,ajp,fcgi}: don't reuse backend connections with data available before the request is sent. PR 57832. [Yann Ylavic]

*) mod_proxy_balancer: Prevent redirect loops between workers within a balancer by limiting the number of redirects to the number balancer members. PR 59864 [Ruediger Pluem]

*) mod_proxy: Correctly consider error response codes by the backend when processing failonstatus. PR 59869 [Ruediger Pluem]

*) mod_dav: Add dav_get_provider_name() function to obtain the name of the provider from mod_dav. [Graham Leggett]

*) mod_dav: Add support for childtags to dav_error. [Jari Urpalainen < jari.urpalainen nokia.com >]

*) mod_proxy_fcgi: Fix 2.4.23 breakage for mod_rewrite per-dir and query string showing up in SCRIPT_FILENAME. PR59815

*) mod_include: Fix a potential memory misuse while evaluating expressions. PR59844. [Eric Covener]

*) mod_http2: new H2CopyFiles directive that changes treatment of file handles in responses. Necessary in order to fix broken lifetime handling in modules such as mod_wsgi.

*) mod_http2: removing timeouts on master connection while requests are being processed. Requests may timeout, but the master only times out when no more requests are active. [Stefan Eissing]

*) mod_http2: fixes connection flush when answering SETTINGS without any stream open. [Moto Ishizawa @summerwind, Stefan Eissing]

27-September-2016 Changes with Apache 2.4.23 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.2j from 1.0.2i (Changelog) 23-September-2016 Changes with Apache 2.4.23 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.2i from 1.0.2h (Changelog) 4-July-2016 Changes with Apache 2.4.23 Apache Lounge changes:

*) Upgraded nghttp2 to 1.12.0 from 1.9.2 (Changelog)

*) Updgraded libxml2 to 2.9.4 from 2.9.3 (Changelog)

*) Upgraded expat to 2.2.0 from 2.1.0 (Changelog)

*) VC14: Build with Visual Studio 2015 Update 3

*) Updgraded pcre to 8.39 from 8.38 (Changelog)

ASF changes:

*) mod_ssl: reset client-verify state of ssl when aborting renegotiations. [Erki Aring < erkiatExample.ee>, Stefan Eissing]

*) mod_sed: Fix 'x' command processing. [Christophe Jaillet]

*) configure: Fix ./configure edge-case failures around dependencies of mod_proxy_hcheck. [William Rowe, Ruediger Pluem, Jeff Trawick] 20-June-2016 Changes with Apache 2.4.22 (not released) ASF changes:

*) mod_http2: fix for request abort when connections drops, introduced in 1.5.8 16-June-2016 Changes with Apache 2.4.21 (not released) ASF changes:

*) mod_http2: more rigid error handling in DATA frame assembly, leading to deterministic connection errors if assembly fails. [Stefan Eissing, Pal Nilsen < github.com/maedox>]

*) abs: Include OPENSSL_Applink when compiling on Windows, to resolve failures under Visual Studio 2015 and other mismatched MSVCRT flavors. PR59630 [Jan Ehrhardt < phpdev ehrhardt.nl>]

*) mod_ssl: Add "no_crl_for_cert_ok" flag to SSLCARevocationCheck directive to opt-in previous behaviour (2.2) with CRLs verification when checking certificate(s) with no corresponding CRL. [Yann Ylavic]

*) mpm_event, mpm_worker: Fix computation of MinSpareThreads' lower bound according the number of listeners buckets. [Yann Ylavic]

*) Add ap_cstr_casecmpn - placeholder of apr_cstr_casecmp[n] functions for case-insensitive C/POSIX-locale token comparison. [Jim Jagielski, William Rowe, Yann Ylavic, Branko ibej]

*) mod_userdir: Constify and save a few bytes in the conf pool when parsing the "UserDir" directive. [Christophe Jaillet]

*) mod_cache: Fix (max-stale with no '=') and enforce (check integers after '=') Cache-Control header parsing. [Christophe Jaillet]

*) core: Add -DDUMP_INCLUDES configtest option to show the tree of Included configuration files. [Jacob Champion < champion.pxi gmail.com>]

*) mod_proxy_fcgi: Avoid passing a filename of proxy:fcgi:// as SCRIPT_FILENAME to a FastCGI server. PR59618. [Jacob Champion < champion.pxi gmail.com>]

*) mod_dav: Add dav_get_provider_name() function to obtain the name of the provider from mod_dav. [Jari Urpalainen < jari.urpalainen nokia.com>]

*) mod_proxy_http2: properly care for HTTP2 flow control of the frontend connection is HTTP/1.1. [Patch supplied by Evgeny Kotkov]

*) mod_http2: improved cleanup of connection/streams/tasks to always have deterministic order regardless of event initiating it. Addresses reported crashes due to memory read after free issues. [Stefan Eissing]

*) mod_ssl: Correct the interaction between SSLProxyCheckPeerCN and newer SSLProxyCheckPeerName directives since release 2.4.5, such that disabling either disables both, and that enabling either triggers the new, more comprehensive SSLProxyCheckPeerName behavior. Only a single configuration remains to enable the legacy behavior, which is to explicitly disable SSLProxyCheckPeerName, and enable SSLProxyCheckPeerCN. [William Rowe]

*) mod_include: add the < !--#comment ... > syntax in order to include comments in a SSI file. [Christophe Jaillet based on a suggestion from Rob]

*) mod_http2: improved event handling for suspended streams, responses and window updates. [Stefan Eissing]

*) mod_proxy_hcheck: Provide for dynamic background health checks on reverse proxies associated with BalancerMember workers. [Jim Jagielski]

*) mod_http2: Fix async write issue that led to selection of wrong timeout vs. keepalive timeout selection for idle sessions. [Stefan Eissing]

*) mod_http2: checking LimitRequestLine, LimitRequestFields and LimitRequestFieldSize configurated values for incoming streams. Returning HTTP status 431 for too long/many headers fields and 414 for a too long pseudo header. [Stefan Eissing]

*) mod_http2: tracking conn_rec->current_thread on slave connections, so that mod_lua finds the correct one. Fixes PR 59542. [Stefan Eissing]

*) mod_proxy_http2: new experimental http2 proxy module for h2: and h2c: proxy urls. Part of the httpd mod_proxy framework, common settings apply. Requests from the same HTTP/2 frontend connection against the same backend are aggregated on a single connection. [Stefan Eissing]

*) mod_http2: slave connections have conn_rec->aborted flag set when a stream has been reset by the client. [Stefan Eissing]

*) mod_http2: merge of some 2.4.x adaptions re filters on slave connections. Small fixes in bucket beams when forwarding file buckets. Output handling on master connection uses less FLUSH and passes automatically when more than half of H2StreamMaxMemSize bytes have accumulated. Workaround for http: when forwarding partial file buckets to keep the output filter from closing these too early. [Stefan Eissing]

*) mod_http2: elimination of fixed master connection buffer for TLS connections. New scratch bucket handling optimized for TLS write sizes. File bucket data read directly into scratch buffers, avoiding one copy. Non-TLS connections continue to pass buckets unchanged to the core filters to allow sendfile() usage. [Stefan Eissing]

*) mod_http2/mod_proxy_http2: h2_request.c is no longer shared between these modules. This simplifies building on platforms such as Windows, as module reference used in logging is now clear. [Stefan Eissing]

*) Scoreboard: Fix a regression in 2.4.20 that causes wrong request data to be displayed on the status page. PR 59333. [Yann Ylavic, William Rowe]

*) mod_http2: fixed a bug that caused mod_proxy_http2 to be called for window updates on requests it had already reported done. Added synchronization on early connection/stream close that lets ongoing requests safely drain their input filters. [Stefan Eissing]

*) mod_http2: scoreboard updates that summarize the h2 session (and replace the last request information) will only happen when the session is idle or in shutdown/done phase. [Stefan Eissing]

*) mod_http2: new "bucket beam" technology to transport buckets across threads without buffer copy. Delaying response start until flush or enough body data has been accumulated. Overall significantly smaller memory footprint. [Stefan Eissing]

*) core: New CGIVar directive can configure REQUEST_URI to represent the current URI being processed instead of always the original request. [Jeff Trawick]

*) scoreboard/status: Restore behavior of showing workers' previous Client, VHost and Request values when idle, like in 2.4.18 and earlier.

*) mod_http2: r->protocol changed to "HTTP/2.0" (was "HTTP/2") as this will give expected syntax in CGI's SERVER_PROTOCOL is more compatible with existing major/minor handling. Fixes PR 59313.

*) mod_http2: disabling mmap for file buckets transport due to segmenation faults when files change on the fly. 4-May-2016 Changes with Apache 2.4.20 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.2h from 1.0.2g (Changelog) 8-April-2016 Changes with Apache 2.4.20 Apache Lounge changes:

*) Upgraded nghttp2 to 1.9.2 from 1.5.0 (Changelog)

ASF changes:

*) core: Do not read .htaccess if AllowOverride and AllowOverrideList are "None". PR 58528. [Michael Schlenker < msc contact.de, Ruediger Pluem, Daniel Ruggeri]

*) mod_proxy_express: Fix possible use of DB handle after close. PR 59230. [Petr < pgajdos suse.cz>]

*) core/util_script: relax alphanumeric filter of enviroment variable names on Windows to allow '(' and ')' for passing PROGRAMFILES(X86) et.al. unadulterated in 64 bit versions of Windows. PR 46751.
[John < john leineweb de>]

*) mod_http2: incrementing keepalives on each request started so that logging %k gives increasing numbers per master http2 connection. New documented variables in env, usable in custom log formats: H2_PUSH, H2_PUSHED, H2_PUSHED_ON, H2_STREAM_ID and H2_STREAM_TAG. [Stefan Eissing]

*) mod_http2: more efficient passing of response bodies with less contention and file bucket forwarding. [Stefan Eissing]

*) mod_http2: fix for missing score board updates on request count, fix for memory leak on slave connection reuse. [Stefan Eissing]

*) mod_http2: Fix build on Windows from dsp files. [Stefan Eissing] 21-March-2016 Changes with Apache 2.4.19 (not released) ASF changes:

*) mod_include: Add variable DOCUMENT_ARGS, with the arguments to the request for the SSI document. [Jeff Trawick]

*) mod_authz_host: Add a new "forward-dns" authorization type, not relying on reverse DNS lookups. [Fabien]

*) mod_ssl: Add hooks to allow other modules to perform processing at several stages of initialization and connection handling. See mod_ssl_openssl.h. [Jeff Trawick]

*) mod_http2: disabling PUSH when client sends GOAWAY. Slave connections are reused for several requests, improved performance and better memory use. [Stefan Eissing]

*) mod_rewrite: Don't implicitly URL-escape the original query string when no substitution has changed it (like PR50447 but server context) [Evgeny Kotkov < evgeny.kotkov visualsvn.com>]

*) mod_http2: fixes problem with wrong lifetime of file buckets on main connection. [Stefan Eissing]

*) mod_http2: fixes incorrect denial of requests without :authority header. [Stefan Eissing]

*) mod_reqtimeout: Prevent long response times from triggering a timeout once the request has been fully read. PR 59045. [Yann Ylavic]

*) ap_expr: expression support for variable HTTP2=on|off. [Stefan Eissing]

*) mod_http2: give control to async mpm for keepalive timeouts only when no streams are open and even if only after 1 sec delay. Under load, event mpm discards connections otherwise too quickly. [Stefan Eissing]

*) mod_ssl: Don't lose track of the SSL context if an unlikely failure occurs in ssl_init_ssl_connection(). [Graham Leggett]

*) mod_rewrite: Add QSL|qslast flag to allow rewrites to files with literal question marks in their names. PR 58777. [Eric Covener]

*) event: use pre_connection hook to properly initialize connection state for slave connections. use protocol_switch hook to initialize server config early based on SNI selected vhost. [Stefan Eissing]

*) hostname: Test and log useragent_host per-request across various modules, including the scoreboard, expression and rewrite engines, setenvif, authz_host, access_compat, custom logging, ssl and REMOTE_HOST variables. PR55348 [William Rowe]

*) core: Track the useragent_host per-request when mod_remoteip or similar modules track a per-request useragent_ip. Modules should be updated to inquire for ap_get_useragent_host() in place of ap_get_remote_host(). [William Rowe]

*) core: fix a bug in < UnDefine ...> directive processing. When used, the last < Define...>'ed variable was also withdrawn. PR 59019 [Christophe Jaillet]

*) mod_http2: Accept-Encoding is, when present on the initiating request, added to push promises. This lets compressed content work in pushes. by the client. [Stefan Eissing]

*) mod_http2: fixed possible read after free when streams were cancelled early by the client. [Stefan Eissing]

*) mod_http2: fixed possible deadlock during connection shutdown. Thanks to @FrankStolle for reporting and getting the necessary data. [Stefan Eissing]

*) mod_http2: fixed apr_uint64_t formatting in a log statement to user proper APR def, thanks to @Sp1l.

) mod_http2: number of worker threads allowed to a connection is adjusting dynamically. Starting with 4, the number is doubled when streams can be served without block on http/2 connection flow. The number is halfed, when the server has to wait on client flow control grants. This can happen with a maximum frequency of 5 times per second. When a connection occupies too many workers, repeatable requests (GET/HEAD/OPTIONS) are cancelled and placed back in the queue. Should that not suffice and a stream is busy longer than the server timeout, the connection will be aborted with error code ENHANCE_YOUR_CALM. This does *not limit the number of streams a client may open, rather the number of server threads a connection might use. [Stefan Eissing]

*) mod_http2: allowing link header to specify multiple "rel" values, space-separated inside a quoted string. Prohibiting push when Link parameter "nopush" is present. [Stefan Eissing]

*) mod_http2: reworked connection state handling. Idle connections accept a GOAWAY from the client without further reply. Otherwise the module makes a best effort to send one last GOAWAY to the client.

*) mod_http2: the values from standard directives Timeout and KeepAliveTimeout properly are applied to http/2 connections. [Stefan Eissing]

*) mod_http2: idle connections are returned to async mpms. new hook "pre_close_connection" used to send GOAWAY frame when not already done. Setting event mpm server config "by hand" for the main connection to the correct negotiated server. [Stefan Eissing]

*) mod_http2: keep-alive blocking reads are done with 1 second timeouts to check for MPM stopping. Will announce early GOAWAY and finish processing open streams, then close. [Stefan Eissing]

*) mod_http2: bytes read/written on slave connections are reported via the optional mod_logio functions. Fixes PR 58871.

*) prefork: Initialize the POD when running in ONE_PROCESS (or -X) mode to avoid a crash. [Jan Kaluza, Yann Ylavic]

*) mod_ssl: When SSLVerify is disabled (NONE), don't force a renegotiation if the SSLVerifyDepth applied with the default/handshaken vhost differs from the one applicable with the finally selected vhost. [Yann Ylavic]

*) core: Ensure that httpd exits with an error status when the MPM fails to run. [Yann Ylavic]

*) mod_ssl: Fix a possible memory leak on restart for custom [EC]DH params. [Jan Kaluza, Yann Ylavic]

*) mod_ssl: Add SSLOCSPProxyURL to add the possibility to do all queries to OCSP responders through a HTTP proxy. [Ruediger Pluem]

*) mod_proxy: Play/restore the TLS-SNI on new backend connections which had to be issued because the remote closed the previous/reusable one during idle (keep-alive) time. [Yann Ylavic]

*) mod_cache_socache: Fix a possible cached entity body corruption when it is received from an origin server in multiple batches and forwarded by mod_proxy. [Yann Ylavic]

*) core: Add expression support to SetHandler. [Eric Covener]

*) mod_remoteip: Prevent an external proxy from presenting an internal proxy. PR 55962. [Mike Rumph]

*) core: Prevent a server crash in case of an invalid CONNECT request with a custom error page for status code 400 that uses server side includes. PR 58929 [Ruediger Pluem]

*) mod_ssl: handle TIMEOUT on empty SSL input as non-fatal, returning APR_TIMEUP and preserving connection state for later retry. [Stefan Eissing]

*) mod_ssl: Save some TLS record (application data) fragmentations by including the last and subsequent suitable buckets when coalescing. [Yann Ylavic]

*) mod_proxy_fcgi: Suppress HTTP error 503 and message 01075, "Error dispatching request", when the cause appears to be due to the client closing the connection. PR58118. [Tobias Adolph < adolph lrz.de>]

*) mod_cgid: Message AH02550, failure to flush a response to the client, is now logged at TRACE1 level to match the underlying core output filter severity. [Eric Covener]

*) mime.types: add common extension "m4a" for MPEG 4 Audio. PR 57895 [Dylan Millikin < dylan.millikin gmail.com>]

*) Added many log numbers to log statements that had none. [Rainer Jung]

*) mod_log_config: Add GlobalLog to allow a globally defined log to be inherited by virtual hosts that define a CustomLog. [Edward Lu]

*) mod_http2: connections how keep a "push diary" where hashes of already pushed resources are kept. See directive H2PushDiarySize for managing this. Push diaries can be initialized by clients via the "Cache-Digest" request header. This carries a base64url encoded. compressed Golomb set as described in https://datatracker.ietf.org/doc/draft-kazuho-h2-cache-digest/Introduced a status handler for HTTP/2 connections, giving various counters and statistics about the current connection, plus its cache digest value in a JSON record. Not a replacement for more HTTP/2 in the server status. Configured as < Location "/http2-status"> SetHandler http2-status < /Location> [Stefan Eissing]

*) mod_http2: Fixed flushing of last GOAWAY frame. Previously, that frame did not always reach the client, causing some to fail the next request. Fixed calculation of last stream id accepted as described in rfc7540. Reading in KEEPALIVE state now correctly shown in scoreboard. Fixed possible race in connection shutdown after review by Ylavic. Fixed segfault on connection shutdown, callback ran into a semi dismantled session. [Stefan Eissing]

*) mod_http2: Added support for experimental accept-push-policy draft (https://tools.ietf.org/html/draft-ruellan-http-accept-push-policy-00). Clients may now influence server pushes by sending accept-push-policy headers. [Stefan Eissing]

*) mod_http2: new r->subprocess_env variables HTTP2 and H2PUSH, set to "on" when available for request. [Stefan Eissing]

*) mod_http2: fixed bug in input window size calculation by moving chunked request body encoding into later stage of processing. Fixes PR 58825. [Stefan Eissing]

*) core: new hook "pre_close_connection" which is run before the lingering close of connections is started. This gives protocol handlers one last chance to use a connection before it goes down. [Stefan Eissing]

*) mod_status/scoreboard: showing connection protocol in new column, new ap_update_child_status methods for updating server/description. mod_ssl sets vhost negotiated by servername directly. [Stefan Eissing] 3-March-2016 Changes with Apache 2.4.18 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.2g from 1.0.2f (Changelog) 22-Februari-2016 Changes with Apache 2.4.18 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.2f from 1.0.2e (Changelog) 11-December-2015 Changes with Apache 2.4.18

Apache Lounge changes:

*) VC14: Build with Visual Studio 2015 Update 1 (including dependencies)

*) Upgraded lua to 5.2.4 from 5.1.5 (Changelog)

*) Upgraded nghttp2 to 1.5.0 from 1.3.4 (Changelog)

*) Updgraded libxml2 to 2.9.3 from 2.9.2 (Changelog)

*) Updgraded pcre to 8.38 from 8.37 (Changelog)

*) Upgraded OpenSSL to 1.0.2e from 1.0.2d (Changelog)

ASF changes:

) mod_ssl: for all ssl_engine_vars.c lookups, fall back to master connection if conn_rec itself holds no valid SSLConnRec. Fixes PR58666. [Stefan Eissing]

*) mod_http2: connection level window for flow control is set to protocol maximum of 2GB-1, preventing window exhaustion when sending data on many streams with higher cumulative window size. Reducing write frequency unless push promises need to be flushed. [Stefan Eissing]

*) mod_http2: required minimum version of libnghttp2 is 1.2.1 [Stefan Eissing]

*) mod_proxy_fdpass: Fix AH01153 error when using the default configuration. In earlier version of httpd, you can explicitelly set the 'flusher' parameter to 'flush' as a workaround. (i.e. flusher=flush) Add documentation for the 'flusher' parameter when defining a proxy worker. [Christophe Jaillet]

*) mod_ssl: For the "SSLStaplingReturnResponderErrors off" case, make sure to only staple responses with certificate status "good". [Kaspar Brand]

*) mod_http2: new directive 'H2PushPriority' to allow priority specifications on server pushed streams according to their content-type. [Stefan Eissing]

*) mod_http2: fixes crash on connection abort for a busy connection. fixes crash on a request that did not produce any response. [Stefan Eissing]

*) mod_http2: trailers are sent after reponse body if set in request_rec trailers_out before the end-of-request bucket is sent through the output filters. [Stefan Eissing]

*) mod_http2: incoming trailers (headers after request body) are properly forwarded to the processing engine. [Stefan Eissing]

*) mod_http2: new directive 'H2Push' to en-/disable HTTP/2 server pushes a server/virtual host. Pushes are initiated by the presence of 'Link:' headers with relation 'preload' on a response. [Stefan Eissing]

*) mod_http2: write performance of http2 improved for larger resources, especially static files. [Stefan Eissing]

*) core: if the first HTTP/1.1 request on a connection goes to a server that prefers different protocols, these protocols are announced in a Upgrade: header on the response, mentioning the preferred protocols. [Stefan Eissing]

*) mod_http2: new directives 'H2TLSWarmUpSize' and 'H2TLSCoolDownSecs' to control TLS record sizes during connection lifetime. [Stefan Eissing]

*) mod_http2: new directive 'H2ModernTLSOnly' to enforce security requirements of RFC 7540 on TLS connections. [Stefan Eissing]

*) core: add ap_get_protocol_upgrades() to retrieve the list of protocols that a client could possibly upgrade to. Use in first request on a connection to announce protocol choices. [Stefan Eissing]

*) mod_http2: reworked deallocation on connection shutdown and worker abort. Separate parent pool for all workers. worker threads are joined on planned worker shutdown. [Yann Ylavic, Stefan Eissing]

*) mod_ssl: when receiving requests for other virtual hosts than the handshake server, the SSL parameters are checked for equality. With equal configuration, requests are passed for processing. Any change will trigger the old behaviour of "421 Misdirected Request". SSL now remembers the cipher suite that was used for the last handshake. This is compared against for any vhost/directory cipher specification. Detailed examination of renegotiation is only done when these do not match. Renegotiation is 403ed when a master connection is present. Exact reason is given additionally in a request note. [Stefan Eissing]

*) core: Fix scoreboard crash (SIGBUS) on hardware requiring strict 64bit alignment (SPARC64, PPC64). [Yann Ylavic]

*) mod_cache: Accept HT (Horizontal Tab) when parsing cache related header fields as described in RFC7230. [Christophe Jaillet]

*) core/util_script: making REDIRECT_URL a full URL is now opt-in via new 'QualifyRedirectURL' directive.

*) core: Limit to ten the number of tolerated empty lines between request, and consume them before the pipelining check to avoid possible response delay when reading the next request without flushing. [Yann Ylavic]

*) mod_ssl: Extend expression parser registration to support ssl variables in any expression using mod_rewrite syntax "%{SSL:VARNAME}" or function syntax "ssl(VARNAME)". [Rainer Jung]

11-October-2015 Changes with Apache 2.4.17

Apache Lounge changes:

*) Build with nghttp2 1.3.4 (Changelog)

*) VC10/11 Upgraded OpenSSL to 1.0.2d from 1.0.1p (Changelog)

ASF changes:

*) mod_http2: added donated HTTP/2 implementation via core module. Similar configuration options to mod_ssl. [Stefan Eissing]

*) mod_proxy: don't recyle backend announced "Connection: close" connections to avoid reusing it should the close be effective after some new request is ready to be sent. [Yann Ylavic]

*) mod_substitute: Allow to configure the patterns merge order with the new SubstituteInheritBefore on|off directive. PR 57641 [Marc.Stern < Marc.Stern approach.be>, Yann Ylavic, William Rowe]

*) mod_proxy: Fix ProxySourceAddress binding failure with AH00938. PR 56687. [Arne de Bruijn < apache arbruijn.dds.nl>

*) mod_ssl: Support compilation against libssl built with OPENSSL_NO_SSL3, and change the compiled-in default for SSL[Proxy]Protocol to "all -SSLv3", in accordance with RFC 7568. PR 58349, PR 57120. [Kaspar Brand]

) mod_ssl: append :!aNULL:!eNULL:!EXP to the cipher string settings, instead of prepending !aNULL:!eNULL:!EXP: (as was the case in 2.4.7 and later). Enables support for configuring the SUITEB cipher strings introduced in OpenSSL 1.0.2. PR 58213. [Kaspar Brand]

*) mod_ssl: Add support for extracting the msUPN and dnsSRV forms of subjectAltName entries of type "otherName" into SSL_{CLIENT,SERVER}SAN_OTHER{msUPN,dnsSRV}_n environment variables. Addresses PR 58020. [Jan Pazdziora < jpazdziora redhat.com>, Kaspar Brand]

*) mod_logio: Fix logging of %^FB (time to first byte) on the first request on an SSL connection. PR 58454.
[Konstantin J. Chernov < k.j.chernov gmail.com>]

*) mod_cache: r->err_headers_out is not merged into r->headers when mod_cache is enabled and the response is cached for the first time. [Edward Lu]

*) mod_slotmem_shm: Fix slots/SHM files names on restart for systems that can't create new (clear) slots while previous children gracefully stopping still use the old ones (e.g. Windows, OS2). mod_proxy_balancer failed to restart whenever the number of configured balancers/members changed during restart. PR 58024. [Yann Ylavic]

*) core/util_script: make REDIRECT_URL a full URL. PR 57785. [Nick Kew]

*) MPMs: Support SO_REUSEPORT to create multiple duplicated listener records for scalability. [Yingqi Lu < yingqi.lu intel.com>, Jeff Trawick, Jim Jagielski, Yann Ylavic]

*) mod_proxy: Fix a race condition that caused a failed worker to be retried before the retry period is over. [Ruediger Pluem]

*) mod_autoindex: Allow autoindexes when neither mod_dir nor mod_mime are loaded. [Eric Covener]

*) mod_rewrite: Allow cookies set by mod_rewrite to contain ':' by accepting ';' as an alternate separator. PR47241. [< bugzilla schermesser com>, Eric Covener]

*) apxs: Add HTTPD_VERSION and HTTPD_MMN to the variables available with apxs -q. PR58202. [Daniel Shahaf < danielsh apache.org>]

*) mod_rewrite: Avoid a crash when lacking correct DB access permissions when using RewriteMap with MapType dbd or fastdbd. [Christophe Jaillet]

*) mod_authz_dbd: Avoid a crash when lacking correct DB access permissions. PR 57868. [Jose Kahan < jose w3.org>, Yann Ylavic]

*) mod_socache_memcache: Add the 'MemcacheConnTTL' directive to control how long to keep idle connections with the memcache server(s). Change default value from 600 usec (!) to 15 sec. PR 58091 [Christophe Jaillet]

*) mod_dir: Prevent the internal identifier "httpd/unix-directory" from appearing as a Content-Type response header when requests for a directory are rewritten by mod_rewrite. [Eric Covener]

22-July-2015 Changes with Apache 2.4.16

Apache Lounge changes:

*) VC14 : Build with the final Visual Studio 2015

14-July-2015 Changes with Apache 2.4.16

Apache Lounge changes:

*) Upgraded APR to 1.5.2 from 1.5.1 (Changelog)

*) httpd.exe build with OPENSSL_Applink shim

*) Added APR OpenSSL Crypto Driver

*) VC14: httpd.exe build with SupportedOS Manifest

*) VC11/10: Updgraded pcre to 8.37 from 8.36 (Changelog)

*) VC14: Upgraded OpenSSL to 1.0.2d from 1.0.2a (Changelog)

*) VC11/10: Upgraded OpenSSL to 1.0.1p from 1.0.1m (Changelog)

ASF changes:

*) http: Fix LimitRequestBody checks when there is no more bytes to read. [Michael Kaufmann mail michael-kaufmann.ch]

*) mod_alias: Revert expression parser support for Alias, ScriptAlias and Redirect due to a regression (introduced in 2.4.13, not released).

*) mod_reqtimeout: Don't let pipelining checks and keep-alive times interfere with the timeouts computed for subsequent requests. PR 56729. [Eric Covener, Yann Ylavic]

*) core: Avoid a possible truncation of the faulty header included in the HTML response when LimitRequestFieldSize is reached. [Yann Ylavic]

*) mod_ldap: In some case, LDAP_NO_SUCH_ATTRIBUTE could be returned instead of an error during a compare operation. [Eric Covener]

19-June-2015 Changes with Apache 2.4.15 (not released)

ASF changes:

*) mod_ext_filter, mod_charset_lite: Avoid inadvertent filtering of protocol data during read of chunked request bodies. PR 58049. [Edward Lu Chaosed0 gmail.com>]

*) mod_ldap: Stop leaking LDAP connections when 'LDAPConnectionPoolTTL 0' is configured. PR 58037. [Ted Phelps phelps gnusto.com>]

*) core: Allow spaces after chunk-size for compatibility with implementations using a pre-filled buffer. [Yann Ylavic, Jeff Trawick]

*) mod_ssl: Remove deprecated SSLCertificateChainFile warning. [Yann Ylavic]

11-June-2015 Changes with Apache 2.4.14 (not released)

ASF changes:

*) SECURITY: CVE-2015-3183 (cve.mitre.org) core: Fix chunk header parsing defect. Remove apr_brigade_flatten(), buffering and duplicated code from the HTTP_IN filter, parse chunks in a single pass with zero copy. Limit accepted chunk-size to 2^63-1 and be strict about chunk-ext authorized characters. [Graham Leggett, Yann Ylavic]

*) SECURITY: CVE-2015-3185 (cve.mitre.org) Replacement of ap_some_auth_required (unusable in Apache httpd 2.4) with new ap_some_authn_required and ap_force_authn hook. [Ben Reser]

4-June-2015 Changes with Apache 2.4.13 (not released) ASF changes:

*) SECURITY: CVE-2015-0253 (cve.mitre.org) core: Fix a crash with ErrorDocument 400 pointing to a local URL-path with the INCLUDES filter active, introduced in 2.4.11. PR 57531. [Yann Ylavic]

*) SECURITY: CVE-2015-0228 (cve.mitre.org) mod_lua: A maliciously crafted websockets PING after a script calls r:wsupgrade() can cause a child process crash. [Edward Lu Chaosed0 gmail.com]

*) mod_proxy: Don't put the worker in error state for 500 or 503 errors returned by the backend unless failonstatus is configured to. PR 56925. [Yann Ylavic]

*) core: Don't lowercase the argument to SetHandler if it begins with "proxy:unix". PR 57968. [Eric Covener]

*) mod_ssl OCSP Stapling: Don't block initial handshakes while refreshing the OCSP response for a different certificate. mod_ssl has an additional global mutex, "ssl-stapling-refresh". PR 57131 (partial fix). [Jeff Trawick]

*) mod_authz_dbm: Fix crashes when "dbm-file-group" is used and authz modules were loaded in the "wrong" order. [Joe Orton]

*) mod_authn_dbd, mod_authz_dbd, mod_session_dbd, mod_rewrite: Fix lifetime of DB lookup entries independently of the selected DB engine. PR 46421. [Steven whitson steven.whitson gmail com, Jan Kaluza, Yann Ylavic].

*) In alignment with RFC 7525, the default recommended SSLCipherSuite and SSLProxyCipherSuite now exclude RC4 as well as MD5. Also, the default recommended SSLProtocol and SSLProxyProtocol directives now exclude SSLv3. Existing configurations must be adjusted by the administrator. [William Rowe]

*) mod_ssl: Add support for extracting subjectAltName entries of type rfc822Name and dNSName into SSL_{CLIENT,SERVER}SAN{Email,DNS}_n environment variables. Also addresses PR 57207. [Kaspar Brand]

*) dav_validate_request: avoid validating locks and ETags when there are no If headers providing them on a resource we aren't modifying. [Ben Reser]

*) mod_proxy_scgi: ProxySCGIInternalRedirect now allows an alternate response header to be used by the application, for when the application or framework is unable to return Location in the internal-redirect form. [Jeff Trawick]

*) core: Cleanup the request soon/even if some output filter fails to handle the EOR bucket. [Yann Ylavic]

*) mpm_event: Allow for timer events duplicates. [Jim Jagielski, Yann Ylavic]

) mod_proxy, mod_ssl, mod_cache_socache, mod_socache_: Support machine readable server-status produced when using the "auto" query string. [Rainer Jung]

*) mod_status: Add more data to machine readable server-status produced when using the "auto" query string. [Rainer Jung]

*) mod_ssl: Check for the Entropy Gathering Daemon (EGD) availability at configure time (RAND_egd), and complain if SSLRandomSeed requires using it otherwise. [Bernard Spil pil.oss gmail com, Stefan Sperling, Kaspar Brand]

*) mod_ssl: make sure to consistently output SSLCertificateChainFile deprecation warnings, when encountered in a VirtualHost block. [Falco Schwarz hiding falco.me]

*) mod_log_config: Add "%{UNIT}T" format to output request duration in seconds, milliseconds or microseconds depending on UNIT ("s", "ms", "us"). [Ben Reser, Rainer Jung]

*) Allow FallbackResource to work when a directory is requested and there is no autoindex nor DirectoryIndex. [Jack tjerk.meesters gmail.com, Eric Covener]

*) mod_proxy_wstunnel: Bypass the handler while the connection is not upgraded to WebSocket, so that other modules can possibly take over the leading HTTP requests. [Yann Ylavic]

*) mod_http: Fix incorrect If-Match handling. PR 57358 [Kunihiko Sakamoto ksakamoto google.com]

*) mod_ssl: Add a warning if protocol given in SSLProtocol or SSLProxyProtocol will override other parameters given in the same directive. This could be a missing + or - prefix. PR 52820 [Christophe Jaillet]

*) core, modules: Avoid error response/document handling by the core if some handler or input filter already did it while reading the request (causing a double response body). [Yann Ylavic]

*) mod_proxy_ajp: Fix client connection errors handling and logged status when it occurs. PR 56823. [Yann Ylavic]

*) mod_proxy: Use the correct server name for SNI in case the backend SSL connection itself is established via a proxy server. PR 57139 [Szabolcs Gyurko szabolcs gyurko.org]

*) mod_ssl: Fix possible crash when loading server certificate constraints. PR 57694. [Paul Spangler paul.spangler ni com, Yann Ylavic]

*) build: Don't load both mod_cgi and mod_cgid in the default configuration if they're both built. [olli hauer ohauer gmx.de]

*) mod_logio: Add LogIOTrackTTFB and %^FB logformat to log the time taken to start writing response headers. [Eric Covener]

*) mod_ssl: Avoid compilation errors with LibreSSL related to the use of ENGINE_CTRL_CHIL_SET_FORKCHECK. [Stuart Henderson sthen openbsd.org]

*) mod_proxy_http: Use the "Connection: close" header for requests to backends not recycling connections (disablereuse), including the default reverse and forward proxies. [Yann Ylavic]

*) mod_proxy: Add ap_connection_reusable() for checking if a connection is reusable as of this point in processing. [Jeff Trawick]

*) mod_proxy_wstunnel: Avoid an empty response by failing with 502 (Bad Gateway) when no response is ever received from the backend. [Jan Kaluza]

*) core_filters: Restore/disable TCP_NOPUSH option after non-blocking sendfile. [Yann Ylavic]

*) mod_buffer: Forward flushed input data immediately and avoid (unlikely) access to freed memory. [Yann Ylavic, Christophe Jaillet]

*) core: Add CGIPassAuth directive to control whether HTTP authorization headers are passed to scripts as CGI variables. PR 56855. [Jeff Trawick]

*) core: Initialize scoreboard's used optional functions on graceful restarts to avoid a crash when relocation occurs. PR 57177. [Yann Ylavic]

*) mod_dav: Avoid a potential integer underflow in the lock timeout value sent back to a client. The answer to a LOCK request could be an extremly large integer if the time needed to lock the resource was longer that the requested timeout given in the LOCK request. In such a case, we now answer "Second-0". PR55420 [Christophe Jaillet]

*) mod_cgid: Within the first minute of a server start or restart, allow mod_cgid to retry connecting to its daemon process. Previously, 'No such file or directory: unable to connect to cgi daemon...' could be logged without an actual retry. PR57685. [Edward Lu Chaosed0 gmail.com]

*) mod_proxy: Use the original (non absolute) form of the request-line's URI for requests embedded in CONNECT payloads used to connect SSL backends via a ProxyRemote forward-proxy. PR 55892. [Hendrik Harms hendrik.harms gmail com, William Rowe, Yann Ylavic]

*) http: Make ap_die() robust against any HTTP error code and not modify response status (finally logged) when nothing is to be done. [Yann Ylavic]

*) mod_proxy_connect/wstunnel: If both client and backend sides get readable at the same time, don't lose errors occuring while forwarding on the first side when none occurs next on the other side, and abort. [Yann Ylavic]

*) mod_rewrite: Improve relative substitutions in per-directory/htaccess context for directories found by mod_userdir and mod_alias. These no longer require RewriteBase to be specified. [Eric Covener]

*) mod_proxy_http: Don't expect the backend to ack the "Connection: close" to finally close those not meant to be kept alive by SetEnv proxy-nokeepalive or force-proxy-request-1.0. [Yann Ylavic]

*) core: If explicitly configured, use the KeepaliveTimeout value of the virtual host which handled the latest request on the connection, or by default the one of the first virtual host bound to the same IP:port. PR56226. [Yann Ylavic]

*) mod_lua: After a r:wsupgrade(), mod_lua was not properly responding to a websockets PING but instead invoking the specified script. PR57524. [Edward Lu Chaosed0 gmail.com>]

*) mod_ssl: Add the SSL_CLIENT_CERT_RFC4523_CEA variable, which provides a combination of certificate serialNumber and issuer as defined by CertificateExactMatch in RFC4523. [Graham Leggett]

*) core: Add expression support to ErrorDocument. Switch from a fixed sized 664 byte array per merge to a hash table. [Graham Leggett]

*) ab: Add missing longest request (100%) to CSV export. [Marcin Fabrykowski bugzilla fabrykowski.pl]

*) mod_macro: Clear macros before initialization to avoid use-after-free on startup or restart when the module is linked statically. PR 57525 [apache.org tech.futurequest.net, Yann Ylavic]

*) mod_alias: Introduce expression parser support for Alias, ScriptAlias and Redirect. [Graham Leggett]

*) mod_ssl: 'SSLProtocol ALL' was being ignored in virtual host context. PR 57100. [Michael Kaufmann apache-bugzilla michael-kaufmann.ch, Yann Ylavic]

*) mpm_event: Avoid access to the scoreboard from the connection while it is suspended (waiting for events). [Eric Covener, Jeff Trawick]

*) mod_ssl: Fix renegotiation failures redirected to an ErrorDocument. PR 57334. [Yann Ylavic].

*) mod_deflate: A misplaced check prevents limiting small bodies with the new inflate limits. PR56872. [Edward Lu, Eric Covener, Yann Ylavic]

*) mod_proxy_ajp: Forward SSL protocol name (SSLv3, TLSv1.1 etc.) as a request attribute to the backend. Recent Tomcat versions will extract it and provide it as a servlet request attribute named "org.apache.tomcat.util.net.secure_protocol_version". [Rainer Jung]

*) core: Optimize string concatenation in expression parser when evaluating a string expression. [Rainer Jung]

*) acinclude.m4: Generate #LoadModule directive in default httpd.conf for every --enable-mpms-shared. PR 53882. [olli hauer ohauer gmx.de> Yann Ylavic]

*) mod_authn_dbd: Fix the error message logged in case of error while querying the database. This is associated to AH01656 and AH01661. [Christophe Jaillet]

*) mod_authz_groupfile: Reduce the severity of AH01667 from ERROR to DEBUG, because it may be evaluated inside RequireAny. PR55523. [Eric Covener]

*) mod_ssl: Fix small memory leak during initialization when ECDH is used. [Jan Kaluza] 27-May-2015 Changes with Apache 2.4.12 Apache Lounge changes:

*) VC14 : Upgraded OpenSSL to 1.0.2a from 1.0.1m (Changelog)

*) VC14 : Updgraded pcre to 8.37 from 8.36 (Changelog)

20-March-2015 Changes with Apache 2.4.12 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.1m from 1.0.1l (Changelog)

*) Upgraded OpenSSL to 0.9.8zf from 1.9.8ze (Changelog)

27-January-2015 Changes with Apache 2.4.12 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.1l from 1.0.1j (Changelog)

*) Upgraded OpenSSL to 0.9.8ze from 1.9.8zc (Changelog)

*) Updgraded pcre to 8.36 from 8.35 (Changelog)

*) PCRE: Build with: SUPPORT_UTF8 and REBUILD_CHARTABLES

*) Upgraded APR-UTIL to 1.5.4 from 1.5.3 (Changelog)

*) Updgraded libxml2 to 2.9.2 from 2.9.1 (Changelog)

ASF changes:

*) Reverted < DirectoryMatch > behavior regression introduced in 2.4.11 (not released).

*) mpm_winnt: Accept utf-8 (Unicode) service names and descriptions for internationalization. [William Rowe]

*) mpm_winnt: Normalize the error and status messages emitted by service.c, the service control interface for Windows. [William Rowe]

*) configure: Fix --enable-v4-mapped configuration on *BSD. PR 53824. [ olli hauer < ohauer gmx.de>, Yann Ylavic ]

15-Januari-2015 Changes with Apache 2.4.11 (not released) Apache Lounge changes:

 None
ASF changes:

*) SECURITY: CVE-2014-3583 (cve.mitre.org) mod_proxy_fcgi: Fix a potential crash due to buffer over-read, with response headers' size above 8K. [Yann Ylavic, Jeff Trawick]

*) SECURITY: CVE-2014-3581 (cve.mitre.org) mod_cache: Avoid a crash when Content-Type has an empty value. PR 56924. [Mark Montague < mark catseye.org>, Jan Kaluza]

*) SECURITY: CVE-2014-8109 (cve.mitre.org) mod_lua: Fix handling of the Require line when a LuaAuthzProvider is used in multiple Require directives with different arguments. PR57204 [Edward Lu < Chaosed0 gmail.com>]

*) SECURITY: CVE-2013-5704 (cve.mitre.org) core: HTTP trailers could be used to replace HTTP headers late during request processing, potentially undoing or otherwise confusing modules that examined or modified request headers earlier. Adds "MergeTrailers" directive to restore legacy behavior. [Edward Lu, Yann Ylavic, Joe Orton, Eric Covener]

*) mod_ssl: New directive SSLSessionTickets (On|Off). The directive controls the use of TLS session tickets (RFC 5077), default value is "On" (unchanged behavior). Session ticket creation uses a random key created during web server startup and recreated during restarts. No other key recreation mechanism is available currently. Therefore using session tickets without restarting the web server with an appropriate frequency (e.g. daily) compromises perfect forward secrecy. [Rainer Jung]

*) mod_proxy_fcgi: Provide some basic alternate options for specifying how PATH_INFO is passed to FastCGI backends by adding significance to the value of proxy-fcgi-pathinfo. PR 55329. [Eric Covener]

*) mod_proxy_fcgi: Enable UDS backends configured with SetHandler/RewriteRule to opt-in to connection reuse and other Proxy options via explicitly declared "proxy workers" (< Proxy unix:... enablereuse=on max=...) [Eric Covener]

*) mod_proxy: Add "enablereuse" option as the inverse of "disablereuse". [Eric Covener]

*) mod_proxy_fcgi: Enable opt-in to TCP connection reuse by explicitly setting proxy option disablereuse=off. [Eric Covener] PR 57378.

*) event: Update the internal "connection id" when requests move from thread to thread. Reuse can confuse modules like mod_cgid. PR 57435. [Michael Thorpe [mike gistnet.com>]

*) mod_proxy_fcgi: Remove proxy:balancer:// prefix from SCRIPT_FILENAME passed to fastcgi backends. [Eric Covener]

*) core: Configuration files with long lines and continuation characters are not read properly. PR 55910. [Manuel Mausz < manuel-as mausz.at>]

*) mod_include: the 'env' function was incorrectly handled as 'getenv' if the leading 'e' was written in upper case in < !--#if expr="..." --> statements. [Christophe Jaillet]

*) split-logfile: Fix perl error: 'Can't use string ("example.org:80") as a symbol ref while "strict refs"'. PR 56329. [Holger Mauermann < mauermann gmail.com>]

*) mod_proxy: Prevent ProxyPassReverse from doing a substitution when the URL parameter interpolates to an empty string. PR 56603. [ ajprout hotmail.com>]

*) core: Fix -D[efined] or < define>[d] variables lifetime accross restarts. PR 57328. [Armin Abfalterer [a.abfalterer gmail.com>, Yann Ylavic].

*) mod_proxy: Preserve original request headers even if they differ from the ones to be forwarded to the backend. PR 45387. [Yann Ylavic]

*) mod_ssl: dump SSL IO/state for the write side of the connection(s), like reads (level TRACE4). [Yann Ylavic]

*) mod_proxy_fcgi: Ignore body data from backend for 304 responses. PR 57198. [Jan Kaluza]

*) mod_ssl: Do not crash when looking up SSL related variables during expression evaluation on non SSL connections. PR 57070 [Ruediger Pluem]

*) mod_proxy_ajp: Fix handling of the default port (8009) in the ProxyPass and < Proxy> configurations. PR 57259. [Yann Ylavic]

*) mpm_event: Avoid a possible use after free when notifying the end of connection during lingering close. PR 57268. [Eric Covener, Yann Ylavic]

*) mod_ssl: Fix recognition of OCSP stapling responses that are encoded improperly or too large. [Jeff Trawick]

*) core: Add ap_log_data(), ap_log_rdata(), etc. for logging buffers. [Jeff Trawick]

*) mod_proxy_fcgi, mod_authnz_fcgi: stop reading the response and issue an error when parsing or forwarding the response fails. [Yann Ylavic]

*) mod_ssl: Fix a memory leak in case of graceful restarts with OpenSSL >= 0.9.8e PR 53435 [tadanori < tadanori2007 yahoo.com>, Sebastian Wiedenroth < wiedi frubar.net>]

*) mod_proxy_connect: Don't issue AH02447 on sockets hangups, let the read determine whether it is a normal close or a real error. PR 57168. [Yann Ylavic]

*) mod_proxy_wstunnel: abort backend connection on polling error to avoid further processing. [Yann Ylavic]

*) core: Support custom ErrorDocuments for HTTP 501 and 414 status codes. PR 57167 [Edward Lu < Chaosed0 gmail.com>]

*) mod_proxy_connect: Fix ProxyRemote to https:// backends on EBCDIC systems. PR 57092 [Edward Lu < Chaosed0 gmail.com>]

*) mod_cache: Avoid a 304 response to an unconditional requst when an AH00752 CacheLock error occurs during cache revalidation. [Eric Covener]

*) mod_ssl: Move OCSP stapling information from a per-certificate store to a per-server hash. PR 54357, PR 56919. [Alex Bligh [alex alex.org.uk>, Yann Ylavic, Kaspar Brand]

*) mod_cache_socache: Change average object size hint from 32 bytes to 2048 bytes. [Rainer Jung]

*) mod_cache_socache: Add cache status to server-status. [Rainer Jung]

*) event: Fix worker-listener deadlock in graceful restart. PR 56960.

*) Concat strings at compile time when possible. PR 53741.

*) mod_substitute: Restrict configuration in .htaccess to FileInfo as documented. [Rainer Jung]

*) mod_substitute: Make maximum line length configurable. [Rainer Jung]

*) mod_substitute: Fix line length limitation in case of regexp plus flatten. [Rainer Jung]

*) mod_proxy: Truncated character worker names are no longer fatal errors. PR53218. [Jim Jagielski]

*) mod_dav: Set r->status_line in dav_error_response. PR 55426.

*) mod_proxy_http, mod_cache: Avoid (unlikely) accesses to freed memory. [Yann Ylavic, Christophe Jaillet]

*) http_protocol: fix logic in ap_method_list_(add|remove) in order: - to correctly reset bits - not to modify the 'method_mask' bitfield unnecessarily [Christophe Jaillet]

*) mod_slotmem_shm: Increase log level for some originally debug messages. [Jim Jagielski]

*) mod_ldap: In 2.4.10, some LDAP searches or comparisons might be done with the wrong credentials when a backend connection is reused. [Eric Covener]

*) mod_macro: Add missing APLOGNO for some Warning log messages. [Christophe Jaillet]

*) mod_cache: Avoid sending 304 responses during failed revalidations PR56881. [Eric Covener]

*) mod_status: Honor client IP address using mod_remoteip. PR 55886. [Jim Jagielski]

*) cmake-based build for Windows: Fix incompatibility with cmake 2.8.12 and later. PR 56615. [Chuck Liu [cliu81 gmail.com], Jeff Trawick]

*) mod_ratelimit: Drop severity of AH01455 and AH01457 (ap_pass_brigade failed) messages from ERROR to TRACE1. Other filters do not bother re-reporting failures from lower level filters. PR56832. [Eric Covener]

*) core: Avoid useless warning message when parsing a section guarded by < IfDefine foo> if $(foo) is used within the section. PR 56503 [Christophe Jaillet]

*) mod_proxy_fcgi: Fix faulty logging of large amounts of stderr from the application. PR 56858. [Manuel Mausz [manuel-asf mausz.at>]

*) mod_proxy_http: Proxy responses with error status and "ProxyErrorOverride On" hang until proxy timeout. PR53420 [Rainer Jung]

*) mod_log_config: Allow three character log formats to be registered. For backwards compatibility, the first character of a three-character format must be the '^' (caret) character. [Eric Covener]

*) mod_lua: Don't quote Expires and Path values. PR 56734. [Keith Mashinter, [kmashint yahoo com>]

*) mod_authz_core: Allow [AuthzProviderAlias>'es to be seen from auth stanzas under virtual hosts. PR 56870. [Eric Covener]

20-October-2014 Changes with Apache 2.4.10 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.1j from 1.0.1i (Changelog)

*) Upgraded OpenSSL to 0.9.8zc from 1.9.8zb (Changelog)

11-August-2014 Changes with Apache 2.4.10 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.1i from 1.0.1h (Changelog)

*) Upgraded OpenSSL to 0.9.8zb from 1.9.8za (Changelog)

17-July-2014 Changes with Apache 2.4.10 Apache Lounge changes:

*) Updgraded pcre to 8.35 from 8.34 (Changelog)

*) Upgraded APR to 1.5.1 from 1.5.0 (Changelog)

ASF changes:

*) SECURITY: CVE-2014-0117 (cve.mitre.org) mod_proxy: Fix crash in Connection header handling which allowed a denial of service attack against a reverse proxy with a threaded MPM. [Ben Reser]

*) SECURITY: CVE-2014-3523 (cve.mitre.org) Fix a memory consumption denial of service in the WinNT MPM (used in all Windows installations). Workaround: AcceptFilter < protocol> {none|connect} [Jeff Trawick]

*) SECURITY: CVE-2014-0226 (cve.mitre.org) Fix a race condition in scoreboard handling, which could lead to a heap buffer overflow. [Joe Orton, Eric Covener]

*) SECURITY: CVE-2014-0118 (cve.mitre.org) mod_deflate: The DEFLATE input filter (inflates request bodies) now limits the length and compression ratio of inflated request bodies to avoid denial of sevice via highly compressed bodies. See directives DeflateInflateLimitRequestBody, DeflateInflateRatioLimit, and DeflateInflateRatioBurst. [Yann Ylavic, Eric Covener]

*) SECURITY: CVE-2014-0231 (cve.mitre.org) mod_cgid: Fix a denial of service against CGI scripts that do not consume stdin that could lead to lingering HTTPD child processes filling up the scoreboard and eventually hanging the server. By default, the client I/O timeout (Timeout directive) now applies to communication with scripts. The CGIDScriptTimeout directive can be used to set a different timeout for communication with scripts. [Rainer Jung, Eric Covener, Yann Ylavic]

*) mod_ssl: Extend the scope of SSLSessionCacheTimeout to sessions resumed by TLS session resumption (RFC 5077). [Rainer Jung]

*) mod_deflate: Don't fail when flushing inflated data to the user-agent and that coincides with the end of stream ("Zlib error flushing inflate buffer"). PR 56196. [Christoph Fausak < christoph fausak glueckkanja.com>]

*) mod_proxy_ajp: Forward local IP address as a custom request attribute like we already do for the remote port. [Rainer Jung]

*) core: Include any error notes set by modules in the canned error response for 403 errors. [Jeff Trawick]

*) mod_ssl: Set an error note for requests rejected due to SSLStrictSNIVHostCheck. [Jeff Trawick]

*) mod_ssl: Fix issue with redirects to error documents when handling SNI errors. [Jeff Trawick]

*) mod_ssl: Fix tmp DH parameter leak, adjust selection to prefer larger keys and support up to 8192-bit keys. [Ruediger Pluem, Joe Orton]

*) mod_dav: Fix improper encoding in PROPFIND responses. PR 56480. [Ben Reser]

*) WinNT MPM: Improve error handling for termination events in child. [Jeff Trawick]

*) mod_proxy: When ping/pong is configured for a worker, don't send or forward "100 Continue" (interim) response to the client if it does not expect one. [Yann Ylavic]

*) mod_ldap: Be more conservative with the last-used time for LDAPConnectionPoolTTL. PR54587 [Eric Covener]

*) mod_ldap: LDAP connections used for authn were not respecting LDAPConnectionPoolTTL. PR54587 [Eric Covener]

*) mod_proxy_fcgi: Fix occasional high CPU when handling request bodies. [Jeff Trawick]

*) event MPM: Fix possible crashes (third-party modules accessing c->sbh) or occasional missed mod_status updates under load. PR 56639. [Edward Lu < Chaosed0 gmail com>]

*) mod_authnz_ldap: Support primitive LDAP servers do not accept filters, such as "SDBM-backed LDAP" on z/OS, by allowing a special filter "none" to be specified in AuthLDAPURL. [Eric Covener]

*) mod_deflate: Fix inflation of files larger than 4GB. PR 56062. [Lukas Bezdicka < social v3.sk>]

*) mod_deflate: Handle Zlib header and validation bytes received in multiple chunks. PR 46146. [Yann Ylavic]

*) mod_proxy: Allow reverse-proxy to be set via explicit handler. [ryo takatsuki < ryotakatsuki gmail com>]

*) ab: support custom HTTP method with -m argument. PR 56604. [Roman Jurkov < winfinit gmail.com>]

*) mod_proxy_balancer: Correctly encode user provided data in management interface. PR 56532 [Maksymilian, < max cert.cx>]

*) mod_proxy_fcgi: Support iobuffersize parameter. [Jeff Trawick]

*) mod_auth_form: Add a debug message when the fields on a form are not recognised. [Graham Leggett]

*) mod_cache: Preserve non-cacheable headers forwarded from an origin 304 response. PR 55547. [Yann Ylavic]

*) mod_proxy_wstunnel: Fix the use of SSL connections with the "wss:" scheme. PR55320. [Alex Liu < alex.leo.ca gmail.com>]

*) mod_socache_shmcb: Correct counting of expirations for status display. Expirations happening during retrieval were not counted. [Rainer Jung]

*) mod_cache: Retry unconditional request with the full URL (including the query-string) when the origin server's 304 response does not match the conditions used to revalidate the stale entry. [Yann Ylavic].

*) mod_alias: Stop setting CONTEXT_PREFIX and CONTEXT_DOCUMENT environment variables as a result of AliasMatch. [Eric Covener]

*) mod_cache: Don't add cached/revalidated entity headers to a 304 response. PR 55547. [Yann Ylavic]

*) mod_proxy_scgi: Support Unix sockets. ap_proxy_port_of_scheme(): Support default SCGI port (4000). [Jeff Trawick]

*) mod_cache: Fix AH00784 errors on Windows when the the CacheLock directive is enabled. [Eric Covener]

*) mod_expires: don't add Expires header to error responses (4xx/5xx), be they generated or forwarded. PR 55669. [Yann Ylavic]

*) mod_proxy_fcgi: Don't segfault when failing to connect to the backend. (regression in 2.4.9 release) [Jeff Trawick]

*) mod_authn_socache: Fix crash at startup in certain configurations. PR 56371. (regression in 2.4.7) [Jan Kaluza]

*) mod_ssl: restore argument structure for "exec"-type SSLPassPhraseDialog programs to the form used in releases up to 2.4.7, and emulate a backwards-compatible behavior for existing setups. [Kaspar Brand]

*) mod_ssl: Add SSLOCSPUseRequestNonce directive to control whether or not OCSP requests should use a nonce to be checked against the responder's one. PR 56233. [Yann Ylavic, Kaspar Brand]

*) mod_ssl: "SSLEngine off" will now override a Listen-based default and does disable mod_ssl for the vhost. [Joe Orton]

*) mod_lua: Enforce the max post size allowed via r:parsebody() [Daniel Gruno]

*) mod_lua: Use binary comparison to find boundaries for multipart objects, as to not terminate our search prematurely when hitting a NULL byte. [Daniel Gruno]

*) mod_ssl: add workaround for SSLCertificateFile when using OpenSSL versions before 0.9.8h and not specifying an SSLCertificateChainFile (regression introduced with 2.4.8). PR 56410. [Kaspar Brand]

*) mod_ssl: bring SNI behavior into better conformance with RFC 6066: no longer send warning-level unrecognized_name(112) alerts, and limit startup warnings to cases where an OpenSSL version without TLS extension support is used. PR 56241. [Kaspar Brand]

*) mod_proxy_html: Avoid some possible memory access violation in case of specially crafted files, when the ProxyHTMLMeta directive is turned on. Follow up of PR 56287 [Christophe Jaillet]

*) mod_auth_form: Make sure the optional functions are loaded even when the AuthFormProvider isn't specified. [Graham Leggett]

*) mod_ssl: avoid processing bogus SSLCertificateKeyFile values (and logging garbled file names). PR 56306. [Kaspar Brand]

*) mod_ssl: fix merging of global and vhost-level settings with the SSLCertificateFile, SSLCertificateKeyFile, and SSLOpenSSLConfCmd directives. PR 56353. [Kaspar Brand]

*) mod_headers: Allow the "value" parameter of Header and RequestHeader to contain an ap_expr expression if prefixed with "expr=". [Eric Covener]

*) rotatelogs: Avoid creation of zombie processes when -p is used on Unix platforms. [Joe Orton]

*) mod_authnz_fcgi: New module to enable FastCGI authorizer applications to authenticate and/or authorize clients. [Jeff Trawick]

*) mod_proxy: Do not try to parse the regular expressions passed by ProxyPassMatch as URL as they do not follow their syntax. PR 56074. [Ruediger Pluem]

*) mod_reqtimeout: Resolve unexpected timeouts on keepalive requests under the Event MPM. PR56216. [Frank Meier < frank meier ergon ch>]

*) mod_proxy_fcgi: Fix sending of response without some HTTP headers that might be set by filters. [Jim Riggs < jim riggs.me>]

*) mod_proxy_html: Do not delete the wrong data from HTML code when a "http-equiv" meta tag specifies a Content-Type behind any other "http-equiv" meta tag. PR 56287 [Micha Lenk < micha lenk info>]

*) mod_proxy: Don't reuse a SSL backend connection whose requested SNI differs. PR 55782. [Yann Ylavic]

*) Add suspend_connection and resume_connection hooks to notify modules when the thread/connection relationship changes. (Should be implemented for any third-party async MPMs.) [Jeff Trawick]

*) mod_proxy_wstunnel: Don't issue AH02447 and log a 500 on routine hangups from websockets origin servers. PR 56299 [Yann Ylavic, Edward Lu < < Chaosed0 gmail com>, Eric Covener]

*) mod_proxy_wstunnel: Don't pool backend websockets connections, because we need to handshake every time. PR 55890. [Eric Covener]

*) mod_lua: Redesign how request record table access behaves, in order to utilize the request record from within these tables. [Daniel Gruno]

*) mod_lua: Add r:wspeek for peeking at WebSocket frames. [Daniel Gruno]

*) mod_lua: Log an error when the initial parsing of a Lua file fails. [Daniel Gruno, Felipe Daragon < filipe syhunt com>]

*) mod_lua: Reformat and escape script error output. [Daniel Gruno, Felipe Daragon < filipe syhunt com>]

*) mod_lua: URL-escape cookie keys/values to prevent tainted cookie data from causing response splitting. [Daniel Gruno, Felipe Daragon < filipe syhunt com>]

*) mod_lua: Disallow newlines in table values inside the request_rec, to prevent HTTP Response Splitting via tainted headers. [Daniel Gruno, Felipe Daragon < filipe syhunt com>]

*) mod_lua: Remove the non-working early/late arguments for LuaHookCheckUserID. [Daniel Gruno]

*) mod_lua: Change IVM storage to use shm [Daniel Gruno]

*) mod_lua: More verbose error logging when a handler function cannot be found. [Daniel Gruno]

5-June-2014 Changes with Apache 2.4.9 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.1h from 1.0.1g (Changelog)

*) Upgraded OpenSSL to 0.9.8za from 1.9.8y (Changelog)

8-April-2014 Changes with Apache 2.4.9 Apache Lounge change:

*) Upgraded OpenSSL to 1.0.1g from 1.0.1f (Changelog)

16-March-2014 Changes with Apache 2.4.9 ASF changes:

*) mod_ssl: Work around a bug in some older versions of OpenSSL that would cause a crash in SSL_get_certificate for servers where the certificate hadn't been sent. [Stephen Henson]

*) mod_lua: Add a fixups hook that checks if the original < request is intended for LuaMapHandler. This fixes a bug where FallbackResource invalidates the LuaMapHandler directive in certain cases by changing the URI before the map handler code executes [Daniel Gruno, Daniel Ferradal < dferradal gmail com>]. 5-June-2014 Changes with Apache 2.4.9 Apache Lounge changes:

*) Upgraded OpenSSL to 1.0.1h from 1.0.1g (Changelog)

*) Upgraded OpenSSL to 0.9.8za from 1.9.8y (Changelog)

8-April-2014 Changes with Apache 2.4.9 Apache Lounge change:

*) Upgraded OpenSSL to 1.0.1g from 1.0.1f (Changelog)

16-March-2014 Changes with Apache 2.4.9 ASF changes:

*) mod_ssl: Work around a bug in some older versions of OpenSSL that would cause a crash in SSL_get_certificate for servers where the certificate hadn't been sent. [Stephen Henson]

*) mod_lua: Add a fixups hook that checks if the original request is intended for LuaMapHandler. This fixes a bug where FallbackResource in< validates the LuaMapHandler directive in certain cases by changing the URI before the map handler code executes [Daniel Gruno, Daniel Ferradal < dferradal gmail com>]. 11-March-2014 Changes with Apache 2.4.8 (not released) Apache Lounge changes:

*) Updgraded pcre to 8.34 from 8.33 (Changelog)

*) Upgraded OpenSSL to 1.0.1f from 1.0.1e (Changelog)

ASF changes:

*) SECURITY: CVE-2014-0098 < (cve.mitre.org) Clean up cookie logging with fewer redundant string parsing passes. Log only cookies with a value assignment. Prevents segfaults when logging truncated cookies. [William Rowe, Ruediger Pluem, Jim Jagielski]

*) SECURITY: CVE-2013-6438 (cve.mitre.org) mod_dav: Keep track of length of cdata properly when removing leading spaces. Eliminates a potential denial of service from specifically crafted DAV WRITE requests [Amin Tora < Amin.Tora neustar.biz>]

*) core: Support named groups and backreferences within the LocationMatch, DirectoryMatch, FilesMatch and ProxyMatch directives. (Requires non-ancient PCRE library) [Graham Leggett]

*) core: draft-ietf-httpbis-p1-messaging-23 corrections regarding TE/CL conflicts. [Yann Ylavic < ylavic.dev gmail com>, Jim Jagielski]

*) mod_dir: Add DirectoryCheckHandler to allow a 2.2-like behavior, skipping execution when a handler is already set. PR53929. [Eric Covener]

*) mod_ssl: Do not perform SNI / Host header comparison in case of a forward proxy request. [Ruediger Pluem]

*) mod_ssl: Remove the hardcoded algorithm-type dependency for the SSLCertificateFile and SSLCertificateKeyFile directives, to enable future algorithm agility, and deprecate the SSLCertificateChainFile directive (obsoleted by SSLCertificateFile). [Kaspar Brand]

*) mod_rewrite: Add RewriteOptions InheritDown, InheritDownBefore, and IgnoreInherit to allow RewriteRules to be pushed from parent scopes to child scopes without explicitly configuring each child scope. PR56153. [Edward Lu < Chaosed0 gmail com>]

*) prefork: Fix long delays when doing a graceful restart. PR 54852 [Jim Jagielski, Arkadiusz Miskiewicz < arekm maven pl>]

*) FreeBSD: Disable IPv4-mapped listening sockets by default for versions 5+ instead of just for FreeBSD 5. PR 53824. [Jeff Trawick]

*) mod_proxy_wstunnel: Avoid busy loop on client errors, drop message IDs 02445, 02446, and 02448 to TRACE1 from DEBUG. PR 56145. [Joffroy Christen < joffroy.christen solvaxis com>, Eric Covener]

*) mod_remoteip: Correct the trusted proxy match test. PR 54651. [Yoshinori Ehara < yoshinori ehara gmail com>, Eugene L < eugenel amazon com>]

*) mod_proxy_fcgi: Fix error message when an unexpected protocol version number is received from the application. PR 56110. [Jeff Trawick]

*) mod_remoteip: Use the correct IP addresses to populate the proxy_ips field. PR 55972. [Mike Rumph]

*) mod_lua: Update r:setcookie() to accept a table of options and add domain, path and httponly to the list of options available to set. PR 56128 [Edward Lu < Chaosed0 gmail com>, Daniel Gruno]

*) mod_lua: Fix r:setcookie() to add, rather than replace, the Set-Cookie header. PR56105 [Kevin J Walters < kjw ms com>, Edward Lu < Chaosed0 gmail com>]

*) mod_lua: Allow for database results to be returned as a hash with row-name/value pairs instead of just row-number/value. [Daniel Gruno]

*) mod_rewrite: Add %{CONN_REMOTE_ADDR} as the non-useragent counterpart to %{REMOTE_ADDR}. PR 56094. [Edward Lu < Chaosed0 gmail com>]

*) WinNT MPM: If ap_run_pre_connection() fails or sets c->aborted, don't save the socket for reuse by the next worker as if it were an APR_SO_DISCONNECTED socket. Restores 2.2 behavior. [Eric Covener]

*) mod_dir: Don't search for a DirectoryIndex or DirectorySlash on a URL that was just rewritten by mod_rewrite. PR53929. [Eric Covener]

*) mod_session: When we have a session we were unable to decode, behave as if there was no session at all. [Thomas Eckert < thomas.r.w.eckert gmail com>]

*) mod_session: Fix problems interpreting the SessionInclude and SessionExclude configuration. PR 56038. [Erik Pearson < erik adaptations.com>]

*) mod_authn_core: Allow < AuthnProviderAlias>'es to be seen from auth stanzas under virtual hosts. PR 55622. [Eric Covener]

*) mod_proxy_fcgi: Use apr_socket_timeout_get instead of hard-coded 30 seconds timeout. [Jan Kaluza]

) build: only search for modules (config.m4) in known subdirectories, see build/config-stubs. [Stefan Fritsch]

*) mod_cache_disk: Fix potential hangs on Windows when using mod_cache_disk. PR 55833. [Eric Covener]

*) mod_ssl: Add support for OpenSSL configuration commands by introducing the SSLOpenSSLConfCmd directive. [Stephen Henson, Kaspar Brand]

*) mod_proxy: Remove (never documented) < Proxy ~ wildcard-url> syntax which is equivalent to < ProxyMatch wildcard-url>. [Christophe Jaillet]

*) mod_authz_user, mod_authz_host, mod_authz_groupfile, mod_authz_dbm, mod_authz_dbd, mod_authnz_ldap: Support the expression parser within the require directives. [Graham Leggett]

*) mod_proxy_http: Core dumped under high load. PR 50335. [Jan Kaluza < jkaluza redhat.com>]

*) mod_socache_shmcb.c: Remove arbitrary restriction on shared memory size previously limited to 64MB. [Jens Låås < jelaas gmail.com>]

*) mod_lua: Use binary copy when dealing with uploads through r:parsebody() to prevent truncating files. [Daniel Gruno] 22-November-2013 Changes with Apache 2.4.7 Apache Lounge changes:

*) Upgraded APR to 1.5.0 from 1.4.8 (Changelog)

*) Upgraded APR-UTIL to 1.5.3 from 1.5.2 (Changelog)

*) VC11: Build with Visual Studio update 4

*) VC11: PCRE Jit enabled

ASF changes:

*) APR 1.5.0 or later is now required for the event MPM.

*) slotmem_shm: Error detection. [Jim Jagielski]

*) event: Use skiplist data structure. [Jim Jagielski]

) mpm_unix: Add ap_mpm_podx_ implementation to avoid code duplication and align w/ trunk. [Jim Jagielski]

*) Fix potential rejection of valid MaxMemFree and ThreadStackSize directives. [Mike Rumph mike.rumph oracle.com]

*) mod_proxy_fcgi: Remove< 64K limit on encoded length of all envvars. An individual envvar with an encoded length of more than 16K will be omitted. [Jeff Trawick]

*) mod_proxy_fcgi: Handle reading protocol data that is split between packets. [Jeff Trawick]

*) mod_ssl: Improve handling of ephemeral DH and ECDH keys by allowing custom parameters to be configured via SSLCertificateFile, and by adding standardized DH parameters for 1024/2048/3072/4096 bits. Unless custom parameters are configured, the standardized parameters are applied based on the certificate's RSA/DSA key size. [Kaspar Brand]

*) mod_ssl, configure: Require OpenSSL 0.9.8a or later. [Kaspar Brand]

*) mod_ssl: drop support for export-grade ciphers with ephemeral RSA keys, and unconditionally disable aNULL, eNULL and EXP ciphers (not overridable via SSLCipherSuite). [Kaspar Brand]

*) mod_proxy: Added support for unix domain sockets as the backend server endpoint. This also introduces an unintended incompatibility for third party modules using the mod_proxy proxy_worker_shared structure, especially for balancer lbmethod modules. [Jim Jagielski, Blaise Tarr < blaise tarr gmail com >]

*) Add experimental cmake-based build system for Windows. [Jeff Trawick, Tom Donovan]

*) event MPM: Fix possible crashes (third party modules accessing c->sbh) or occasional missed mod_status updates for some keepalive requests under load. [Eric Covener]

*) mod_authn_socache: Support optional initialization arguments for socache providers. [Chris Darroch]

*) mod_session: Reset the max-age on session save. PR 47476. [Alexey Varlamov alexey.v.varlamov gmail com]

*) mod_session: After parsing the value of the header specified by the SessionHeader directive, remove the value from the response. PR 55279. [Graham Leggett]

*) mod_headers: Allow for format specifiers in the substitution string when using Header edit. [Daniel Ruggeri]

*) mod_dav: dav_resource->uri is treated as unencoded. This was an unnecessary ABI changed introduced in 2.4.6. PR 55397.

*) mod_dav: Don't require lock tokens for COPY source. PR 55306.

*) core: Don't truncate output when sending is interrupted by a signal, such as from an exiting CGI process. PR 55643. [Jeff Trawick]

*) WinNT MPM: Exit the child if the parent process crashes or is terminated. [Oracle Corporation]

*) Windows: Correct failure to discard stderr in some error log configurations. (Error message AH00093) [Jeff Trawick]

*) mod_session_crypto: Allow using exec: calls to obtain session encryption key. [Daniel Ruggeri]

*) core: Add missing Reason-Phrase in HTTP response headers. PR 54946. [Rainer Jung]

*) mod_rewrite: Make rewrite websocket-aware to allow proxying. PR 55598. [Chris Harris chris.harris kitware com]

) mod_ldap: When looking up sub-groups, use an implicit objectClass= instead of an explicit cn=* filter. [David Hawes dhawes vt.edu]

*) ab: Add wait time, fix processing time, and output write errors only if they occured. [Christophe Jaillet]

*) worker MPM: Don't forcibly kill worker threads if the child process is exiting gracefully. [Oracle Corporation]

*) core: apachectl -S prints wildcard name-based virtual hosts twice. PR54948 [Eric Covener]

*) mod_auth_basic: Add AuthBasicUseDigestAlgorithm directive to allow migration of passwords from digest to basic authentication. [Chris Darroch]

*) ab: Add a new -l parameter in order not to check the length of the responses. This can be usefull with dynamic pages. PR9945, PR27888, PR42040 [ccikrs1 cranbrook edu]

*) Suppress formatting of startup messages written to the console when ErrorLogFormat is used. [Jeff Trawick]

*) mod_auth_digest: Be more specific when the realm mismatches because the realm has not been specified. [Graham Leggett]

*) mod_proxy: Add a note in the balancer manager stating whether changes will or will not be persisted and whether settings are inherited. [Daniel Ruggeri, Jim Jagielski]

*) mod_cache: Avoid a crash with strcmp() when the hostname is not provided. [Graham Leggett]

*) core: Add util_fcgi.h and associated definitions and support routines for FastCGI, based largely on mod_proxy_fcgi. [Jeff Trawick]

*) mod_headers: Add 'Header note header-name note-name' for copying a response headers value into a note. [Eric Covener]

*) mod_headers: Add 'setifempty' command to Header and RequestHeader. [Eric Covener]

*) mod_logio: new format-specifier %S (sum) which is the sum of received and sent byte counts. PR54015 [Christophe Jaillet]

*) mod_deflate: Improve error detection when decompressing request bodies with trailing garbage: handle case where trailing bytes are in the same bucket. [Rainer Jung]

*) mod_authz_groupfile, mod_authz_user: Reduce severity of AH01671 and AH01663 from ERROR to DEBUG, since these modules do not know what mod_authz_core is doing with their AUTHZ_DENIED return value. [Eric Covener]

*) mod_ldap: add TRACE5 for LDAP retries. [Eric Covener]

*) mod_ldap: retry on an LDAP timeout during authn. [Eric Covener]

*) mod_ldap: Change "LDAPReferrals off" to actually set the underlying LDAP SDK option to OFF, and introduce "LDAPReferrals default" to take the SDK default, sans rebind authentication callback. [Jan Kaluza kaluze AT redhat.com]

*) core: Log a message at TRACE1 when the client aborts a connection. [Eric Covener]

*) WinNT MPM: Don't crash during child process initialization if the Listen protocol is unrecognized. [Jeff Trawick]

*) modules: Fix some compiler warnings. [Guenter Knauf]

*) Sync 2.4 and trunk - Avoid some memory allocation and work when TRACE1 is not activated - fix typo in include guard - indent - No need to lower the string before removing the path, it is just a waste of time... - Save a few cycles [Christophe Jaillet christophe.jaillet wanadoo.fr]

*) mod_filter: Add "change=no" as a proto-flag to FilterProtocol to remove a providers initial flags set at registration time. [Eric Covener]

*) core, mod_ssl: Enable the ability for a module to reverse the sense of a poll event from a read to a write or vice versa. This is a step on the way to allow mod_ssl taking full advantage of the event MPM. [Graham Leggett]

*) Makefile.win: Install proper pcre DLL file during debug build install. PR 55235. [Ben Reser ben reser org]

*) mod_ldap: Fix a potential memory leak or corruption. PR 54936. [Zhenbo Xu zhenbo1987 gmail com]

*) ab: Fix potential buffer overflows when processing the T and X command-line options. PR 55360. [Mike Rumph mike.rumph oracle.com]

*) fcgistarter: Specify SO_REUSEADDR to allow starting a server with old connections in TIME_WAIT. [Jeff Trawick]

*) core: Add open_htaccess hook which, in conjunction with dirwalk_stat and post_perdir_config (introduced in 2.4.5), allows mpm-itk to be used without patches to httpd core. [Stefan Fritsch]

*) support/htdbm: fix processing of -t command line switch. Regression introduced in 2.4.4 PR 55264 [Jo Rhett jrhett netconsonance com]

*) mod_lua: add websocket support via r:wsupgrade, r:wswrite, r:wsread and r:wsping. [Daniel Gruno]

*) mod_lua: add support for writing/reading cookies via r:getcookie and r:setcookie. [Daniel Gruno]

15-July-2013 Changes with Apache 2.4.6 ASF changes:

*) Revert a broken fix for PR54948 that was applied to 2.4.5 (which was not released) and found post-2.4.5 tagging.

12-July-2013 Changes with Apache 2.4.5 (not released) Apache Lounge changes:

*) VC11: Build with Visual Studio update 3

*) Upgraded zlib to 1.2.8 from 1.2.7 (Changelog)

*) Upgraded APR to 1.4.8 from 1.4.6 (Changelog)

*) Upgraded APR-UTIL to 1.5.2 from 1.4.1 (Changelog)

*) Updgraded pcre to 8.33 from 8.32 (Changelog)

*) Updgraded libxml2 to 2.9.1 from 2.9.0 (Changelog)

*) Apache Lounge VC Identification

*) VC11: Upped the windows headers version to 600

ASF changes:

*) new modules: mod_cache_socache, m< od_macro and mod_proxy_wstunnel mod_cache_socache is the mod_mem_cache replacement for Apache 2.4

*) SECURITY: CVE-2013-1896 (cve.mitre.org) mod_dav: Sending a MERGE request against a URI handled by mod_dav_svn with the source href (sent as part of the request body as XML) pointing to a URI that is not configured for DAV will trigger a segfault. [Ben Reser ben reser.org]

*) SECURITY: CVE-2013-2249 (cve.mitre.org) mod_session_dbd: Make sure that dirty flag is respected when saving sessions, and ensure the session ID is changed each time the session changes. This changes the format of the updatesession SQL statement. Existing configurations must be changed. [Takashi Sato takashi tks.st, Graham Leggett]

*) mod_auth_basic: Add a generic mechanism to fake basic authentication using the ap_expr parser. AuthBasicFake allows the administrator to construct their own username and password for basic authentication based on their needs. [Graham Leggett]

*) mpm_event: Check that AsyncRequestWorkerFactor is not negative. PR 54254. [Jackie Zhang jackie qq zhang gmail com]

*) mod_proxy: Ensure we don't attempt to amend a table we are iterating through, ensuring that all headers listed by Connection are removed. [Graham Leggett, Co-Advisor coad measurement-factory.com]

*) mod_proxy_http: Make the proxy-interim-response environment variable effective by formally overriding origin server behaviour. [Graham Leggett, Co-Advisor coad measurement-factory.com]

*) mod_proxy: Fix seg-faults when using the global pool on threaded MPMs [Thomas Eckert thomas.r.w.eckert gmail.com, Graham Leggett, Jim Jagielski]

*) mod_deflate: Remove assumptions as to when an EOS bucket might arrive. Gracefully step aside if the body size is zero. [Graham Leggett]

*) mod_ssl: Fix possible truncation of OCSP responses when reading from the server. [Joe Orton]

*) core: Support the SINGLE_LISTEN_UNSERIALIZED_ACCEPT optimization on Linux kernel versions 3.x and above. PR 55121. [Bradley Heilbrun apache heilbrun.org]

*) mod_cache_socache: Make sure the CacheSocacheMaxSize directive is merged correctly. [Jens Låås jelaas gmail.com]

*) rotatelogs: add -n number-of-files option to roate through a number of fixed-name logfiles. [Eric Covener]

*) mod_proxy: Support web-socket tunnels via mod_proxy_wstunnel. [Jim Jagielski]

*) mod_cache_socache: Use the name of the socache implementation when performing a lookup rather than using the raw arguments. [Martin Ksellmann martin ksellmann.de]

*) core: Add dirwalk_stat hook. [Jeff Trawick]

*) core: Add post_perdir_config hook. [Steinar Gunderson sgunderson bigfoot.com]

*) proxy_util: NULL terminate the right buffer in 'send_http_connect'. [Christophe Jaillet]

*) mod_remoteip: close file in error path. [Christophe Jaillet]

*) core: make the "default" parameter of the "ErrorDocument" option case insensitive. PR 54419 [Tianyin Xu tixu cs ucsd edu]

*) mod_proxy_html: make the "ProxyHTMLFixups" options case insensitive. PR 54420 [Tianyin Xu tixu cs ucsd edu]

*) mod_cache: Make option "CacheDisable" in mod_cache case insensitive. PR 54462 [Tianyin Xu tixu cs ucsd edu]

*) mod_cache: If a 304 response indicates an entity not currently cached, then the cache MUST disregard the response and repeat the request without the conditional. [Graham Leggett, Co-Advisor coad measurement-factory.com]

*) mod_cache: Ensure that we don't attempt to replace a cached response with an older response as per RFC2616 13.12. [Graham Leggett, Co-Advisor coad measurement-factory.com]

*) core, mod_cache: Ensure RFC2616 compliance in ap_meets_conditions() with weak validation combined with If-Range and Range headers. Break out explicit conditional header checks to be useable elsewhere in the server. Ensure weak validation RFC compliance in the byteranges filter. Ensure RFC validation compliance when serving cached entities. PR 16142 [Graham Leggett, Co-Advisor coad measurement-factory.com]

*) core: Add the ability to do explicit matching on weak and strong ETags as per RFC2616 Section 13.3.3. [Graham Leggett, Co-Advisor coad measurement-factory.com]

*) mod_cache: Ensure that updated responses to HEAD requests don't get mistakenly paired with a previously cached body. Ensure that any existing body is removed when a HEAD request is cached. [Graham Leggett, Co-Advisor coad measurement-factory.com]

*) mod_cache: Honour Cache-Control: no-store in a request. [Graham Leggett]

*) mod_cache: Make sure that contradictory entity headers present in a 304 Not Modified response are caught and cause the entity to be removed. [Graham Leggett]

*) mod_cache: Make sure Vary processing handles multivalued Vary headers and multivalued headers referred to via Vary. [Graham Leggett]

*) mod_cache: When serving from cache, only the last header of a multivalued header was taken into account. Fixed. Ensure that Warning headers are correctly handled as per RFC2616. [Graham Leggett]

*) mod_cache: Ignore response headers specified by no-cache=header and private=header as specified by RFC2616 14.9.1 What is Cacheable. Ensure that these headers are still processed when multiple Cache-Control headers are present in the response. PR 54706 [Graham Leggett, Yann Ylavic ylavic.dev gmail.com]

*) mod_cache: Invalidate cached entities in response to RFC2616 Section 13.10 Invalidation After Updates or Deletions. PR 15868 [Graham Leggett]

*) mod_dav: Improve error handling in dav_method_put(), add new dav_join_error() function. PR 54145. [Ben Reser ben reser.org]

*) mod_dav: Do not fail PROPPATCH when prop namespace is not known. PR 52559 [Diego Santa Cruz diego.santaCruz spinetix.com]

*) mod_dav: When a PROPPATCH attempts to remove a non-existent dead property on a resource for which there is no dead property in the same namespace httpd segfaults. PR 52559 [Diego Santa Cruz diego.santaCruz spinetix.com]

*) mod_dav: Sending an If or If-Match header with an invalid ETag doesn't result in a 412 Precondition Failed for a COPY operation. PR54610 [Timothy Wood tjw omnigroup.com]

*) mod_dav: Make sure that when we prepare an If URL for Etag comparison, we compare unencoded paths. PR 53910 [Timothy Wood tjw omnigroup.com]

*) 'AuthGroupFile' and 'AuthUserFile' do not accept anymore the optional 'standard' keyword . It was unused and not documented. PR54463 [Tianyin Xu tixu cs.ucsd.edu and Christophe Jaillet]

*) core: Do not over allocate memory within 'ap_rgetline_core' for the common case. [Christophe Jaillet]

*) core: speed up (for common cases) and reduce memory usage of ap_escape_logitem(). This should save 70-100 bytes in the request pool for a default config. [Christophe Jaillet]

*) mod_dav: Ensure URI is correctly uriencoded on return. PR 54611 [Timothy Wood tjw omnigroup.com]

*) core: apachectl -S prints wildcard name-based virtual hosts twice. PR54948 [Eric Covener]

*) mod_proxy: Reject invalid values for Max-Forwards. [Graham Leggett, Co-Advisor coad measurement-factory.com]

*) mod_cache: RFC2616 14.9.3 The s-maxage directive also implies the semantics of the proxy-revalidate directive. [Graham Leggett]

*) mod_ssl: add support for subjectAltName-based host name checking in proxy mode (SSLProxyCheckPeerName). PR 54030. [Kaspar Brand]

*) core: Use the proper macro for HTTP/1.1. [Graham Leggett]

*) event MPM: Provide error handling for ThreadStackSize. PR 54311 [Tianyin Xu tixu cs.ucsd.edu, Christophe Jaillet]

*) mod_dav: Do not segfault on PROPFIND with a zero length DBM. PR 52559 [Diego Santa Cruz diego.santaCruz spinetix.com]

*) core: Improve error message where client's request-line exceeds LimitRequestLine. PR 54384 [Christophe Jaillet]

*) mod_macro: New module that provides macros within configuration files. [Fabien Coelho]

*) mod_cache_socache: New cache implementation backed by mod_socache that replaces mod_mem_cache known from httpd 2.2. [Graham Leggett]

*) htpasswd: Add -v option to verify a password. [Stefan Fritsch]

*) mod_proxy: Add BalancerInherit and ProxyPassInherit to control whether Proxy Balancers and Workers are inherited by vhosts (default is On). [Jim Jagielski]

*) mod_authnz_ldap: Allow using exec: calls to obtain LDAP bind password. [Daniel Ruggeri]

*) Added balancer parameter failontimeout to allow server admin to configure an IO timeout as an error in the balancer. [Daniel Ruggeri]

*) mod_auth_digest: Fix crashes if shm initialization failed. [Stefan Fritsch]

*) htpasswd, htdbm: Fix password generation. PR 54735. [Stefan Fritsch]

*) core: Add workaround for gcc bug on sparc/64bit. PR 52900. [Stefan Fritsch]

*) mod_setenvif: Fix crash in case SetEnvif and SetEnvIfExpr are used together. PR 54881. [Ruediger Pluem]

*) htdigest: Fix buffer overflow when reading digest password file with very long lines. PR 54893. [Rainer Jung]

*) ap_expr: Add the ability to base64 encode and base64 decode strings and to generate their SHA1 and MD5 hash. [Graham Leggett, Stefan Fritsch]

*) mod_log_config: Fix crash when logging request end time for a failed request. PR 54828 [Rainer Jung]

*) mod_ssl: Catch missing, mismatched or encrypted client cert/key pairs with SSLProxyMachineCertificateFile/Path directives. PR 52212, PR 54698. [Keith Burdis keith burdis.org, Joe Orton, Kaspar Brand]

*) mod_ssl: Quiet FIPS mode weak keys disabled and FIPS not selected emits in the error log to debug level. [William Rowe]

*) mod_cache_disk: CacheMinFileSize and CacheMaxFileSize were always using compiled in defaults of 1000000/1 respectively. [Eric Covener]

*) mod_lbmethod_heartbeat, mod_heartmonitor: Respect DefaultRuntimeDir/ DEFAULT_REL_RUNTIMEDIR for the heartbeat storage file. [Jeff Trawick]

*) mod_include: Use new ap_expr for 'elif', like 'if', if legacy parser is not specified. PR 54548 [Tom Donovan]

*) mod_lua: Add some new functions: r:htpassword(), r:mkdir(), r:mkrdir(), r:rmdir(), r:touch(), r:get_direntries(), r.date_parse_rfc(). [Guenter Knauf]

*) mod_lua: Add multipart form data handling. [Daniel Gruno]

*) mod_lua: If a LuaMapHandler doesn't return any value, log a warning and treat it as apache2.OK. [Eric Covener]

*) mod_lua: Add bindings for apr_dbd/mod_dbd database access [Daniel Gruno]

*) mod_lua: Add LuaInputFilter/LuaOutputFilter for creating content filters in Lua [Daniel Gruno]

*) mod_lua: Allow scripts handled by the lua-script handler to return a status code to the client (such as a 302 or a 500) [Daniel Gruno]

*) mod_lua: Decline handling 'lua-script' if the file doesn't exist, rather than throwing an internal server error. [Daniel Gruno]

*) mod_lua: Add functions r:flush and r:sendfile as well as additional request information to the request_rec structure. [Daniel Gruno]

*) mod_lua: Add a server scope for Lua states, which creates a pool of states with managable minimum and maximum size. [Daniel Gruno]

*) mod_lua: Add new directive, LuaMapHandler, for dynamically mapping URIs to Lua scripts and functions using regular expressions. [Daniel Gruno]

*) mod_lua: Add new directive LuaCodeCache for controlling in-memory caching of lua scripts. [Daniel Gruno]

22-February-2013 Changes with Apache 2.4.4 Apache Lounge changes:

*) VC11 version available

*) Libxml2 upgraded from 2.7.8 to 2.9.0 (Changelog)

*) PCRE upgraded from 8.30 to 8.32 (Changelog)

*) Upgraded OpenSSL from 1.0.1c, 0.9.8x to 1.0.1e, 0.9.8y (Changelog)

*) Win64 Binary apr-1.4.6 patched (ASF PR: 49155) WIN64 wasn't defined correctly in APR, resulting in crashes

*) Upped the windows headers version to 502

ASF changes:<

*) SECURITY: CVE-2012-3499 (cve.mitre.org) Various XSS flaws due to unescaped hostnames and URIs HTML output in mod_info, mod_status, mod_imagemap, mod_ldap, and mod_proxy_ftp. [Jim Jagielski, Stefan Fritsch, Niels Heinen heinenn google com]

*) SECURITY: CVE-2012-4558 (cve.mitre.org) XSS in mod_proxy_balancer manager interface. [Jim Jagielski, Niels Heinen heinenn google com]

*) mod_dir: Add support for the value 'disabled' in FallbackResource. [Vincent Deffontaines]

*) mod_proxy_connect: Don't keepalive the connection to the client if the backend closes the connection. PR 54474. [Pavel Mateja < pavel netsafe cz>]

*) mod_lua: Add bindings for mod_dbd/apr_dbd database access. [Daniel Gruno]

*) mod_proxy: Allow for persistence of local changes made via the balancer-manager between graceful/normal restarts and power cycles. [Jim Jagielski]

*) mod_status: Print out list of times since a Vhost was last used. [Jim Jagielski]

*) mod_proxy: Fix startup crash with mis-defined balancers. PR 52402. [Jim Jagielski]

*) --with-module: Fix failure to integrate them into some existing module directories. PR 40097. [Jeff Trawick]

*) htcacheclean: Fix potential segfault if "-p" is omitted. [Joe Orton]

*) mod_proxy_http: Honour special value 0 (unlimited) of LimitRequestBody PR 54435. [Pavel Mateja < pavel netsafe.cz>]

*) mod_proxy_ajp: Support unknown HTTP methods. PR 54416. [Rainer Jung]

*) htcacheclean: Fix list options "-a" and "-A". [Rainer Jung]

*) mod_slotmem_shm: Fix mistaken reset of num_free for restored shm. [Jim Jagielski]

*) mod_proxy: non-existance of byrequests is not an immediate error. [Jim Jagielski]

*) mod_proxy_balancer: Improve output of balancer-manager (re: Drn, Dis, Ign, Stby). PR 52478 [Danijel < dt-ng rbfh de>]

*) configure: Fix processing of --disable-FEATURE for various features. [Jeff Trawick]

*) mod_dialup/mod_http: Prevent a crash in mod_dialup in case of internal redirect. PR 52230.

*) various modules, rotatelogs: Replace use of apr_file_write() with apr_file_write_full() to prevent incomplete writes. PR 53131. [Nicolas Viennot < apache viennot biz>, Stefan Fritsch]

*) ab: Support socket timeout (-s timeout). [Guido Serra < zeph fsfe org>]

*) httxt2dbm: Correct length computation for the 'value' stored in the DBM file. PR 47650 [jon buckybox com]

*) core: Be more correct about rejecting directives that cannot work in < If> sections. [Stefan Fritsch]

*) core: Fix directives like LogLevel that need to know if they are invoked at virtual host context or in Directory/Files/Location/If sections to work properly in If sections that are not in a Directory/Files/Location. [Stefan Fritsch]

*) mod_xml2enc: Fix problems with charset conversion altering the Content-Length. [Micha Lenk < micha lenk info>]

*) ap_expr: Add req_novary function that allows HTTP header lookups without adding the name to the Vary header. [Stefan Fritsch]

) mod_slotmem_: Add in new fgrab() function which forces a grab and slot allocation on a specified slot. Allow for clearing of inuse array. [Jim Jagielski]

*) mod_proxy_ftp: Fix segfaults on IPv4 requests to hosts with DNS AAAA records. PR 40841. [Andrew Rucker Jones < arjones simultan dyndns org>, < ast domdv de>, Jim Jagielski]

*) mod_auth_form: Make sure that get_notes_auth() sets the user as does get_form_auth() and get_session_auth(). Makes sure that REMOTE_USER does not vanish during mod_include driven subrequests. [Graham Leggett]

*) mod_cache_disk: Resolve errors while revalidating disk-cached files on Windows ("...rename tempfile to datafile failed..."). PR 38827 [Eric Covener]

*) mod_proxy_balancer: Bring XML output up to date. [Jim Jagielski]

*) htpasswd, htdbm: Optionally read passwords from stdin, as more secure alternative to -b. PR 40243. [Adomas Paltanavicius < adomas paltanavicius gmail com>, Stefan Fritsch]

*) htpasswd, htdbm: Add support for bcrypt algorithm (requires apr-util 1.5 or higher). PR 49288. [Stefan Fritsch]

*) htpasswd, htdbm: Put full 48bit of entropy into salt, improve error handling. Add some of htpasswd's improvements to htdbm, e.g. warn if password is truncated by crypt(). [Stefan Fritsch]

*) mod_auth_form: Support the expr parser in the AuthFormLoginRequiredLocation, AuthFormLoginSuccessLocation and AuthFormLogoutLocation directives. [Graham Leggett]

*) mod_ssl: Add support for TLS-SRP (Secure Remote Password key exchange for TLS, RFC 5054). PR 51075. [Quinn Slack < sqs cs stanford edu>, Christophe Renou, Peter Sylvester]

*) mod_rewrite: Stop mergeing RewriteBase down to subdirectories unless new option 'RewriteOptions MergeBase' is configured. PR 53963. [Eric Covener]

*) mod_header: Allow for exposure of loadavg and server load using new format specifiers %l, %i, %b [Jim Jagielski]

*) core: Make ap_regcomp() return AP_REG_ESPACE if out of memory. Make ap_pregcomp() abort if out of memory. This raises the minimum PCRE requirement to version 6.0. [Stefan Fritsch]

*) mod_proxy: Add ability to configure the sticky session separator. PR 53893. [< inu inusasha de>, Jim Jagielski]

*) mod_dumpio: Correctly log large messages PR 54179 [Marek Wianecki < mieszek2 interia pl>]

*) core: Don't fail at startup with AH00554 when Include points to a directory without any wildcard character. [Eric Covener]

*) core: Fail startup if the argument to ServerTokens is unrecognized. [Jackie Zhang < jackie.qq.zhang gmail.com>]

*) mod_log_forensic: Don't log a spurious "-" if a request has been rejected before mod_log_forensic could attach its id to it. [Stefan Fritsch]

*) rotatelogs: Omit the second argument for the first invocation of a post-rotate program when -p is used, per the documentation. [Joe Orton]

*) mod_session_dbd: fix a segmentation fault in the function dbd_remove. PR 53452. [< rebanerebane gmail com>, Reimo Rebane]

*) core: Functions to provide server load values: ap_get_sload() and ap_get_loadavg(). [Jim Jagielski, Jan Kaluza < jkaluza redhat.com>, Jeff Trawick]

*) mod_ldap: Fix regression in handling "server unavailable" errors on Windows. PR 54140. [Eric Covener]

*) syslog logging: Remove stray ", referer" at the end of some messages. [Jeff Trawick]

*) "Iterate" directives: Report an error if no arguments are provided. [Jeff Trawick]

*) mod_ssl: Change default for SSLCompression to off, as compression causes security issues in most setups. (The so called "CRIME" attack). [Stefan Fritsch]

*) ab: add TLS1.1/TLS1.2 options to -f switch, and adapt output to more accurately report the negotiated protocol. PR 53916. [Nicolás Pernas Maradei < nico emutex com>, Kaspar Brand]

*) core: ErrorDocument now works for requests without a Host header. PR 48357. [Jeff Trawick]

*) prefork: Avoid logging harmless errors during graceful stop. [Joe Orton, Jeff Trawick]

*) mod_proxy: When concatting for PPR, avoid cases where we concat ".../" and "/..." to create "...//..." [Jim Jagielski]

*) mod_cache: Wrong content type and character set when mod_cache serves stale content because of a proxy error. PR 53539. [Rainer Jung, Ruediger Pluem]

*) mod_proxy_ajp: Fix crash in packet dump code when logging with LogLevel trace7 or trace8. PR 53730. [Rainer Jung]

*) httpd.conf: Removed the configuration directives setting a bad_DNT environment introduced in 2.4.3. The actual directives are commented out in the default conf file.

*) core: Apply length limit when logging Status header values. [Jeff Trawick, Chris Darroch]

*) mod_proxy_balancer: The nonce is only derived from the UUID iff not set via the 'nonce' balancer param. [Jim Jagielski]

*) mod_ssl: Match wildcard SSL certificate names in proxy mode.
PR 53006. [Joe Orton]

*) Windows: Fix output of -M, -L, and similar command-line options which display information about the server configuration. [Jeff Trawick]

18-August-2012 Changes with Apache 2.4.3 Apache Lounge change:

*) Win64 Binary apr-1.4.6 patched (ASF PR: 49155) WIN64 wasn't defined correctly in APR, resulting in crashes

ASF changes:

*) SECURITY: CVE-2012-3502 (cve.mitre.org) mod_proxy_ajp, mod_proxy_http: Fix an issue in back end connection closing which could lead to privacy issues due to a response mixup. PR 53727. [Rainer Jung] < *) SECURITY: CVE-2012-2687 (cve.mitre.org) mod_negotiation: Escape filenames in variant list to prevent an possible XSS for a site where untrusted users can upload files to a location with MultiViews enabled. [Niels Heinen < heinenn google.com>]

*) mod_authnz_ldap: Don't try a potentially expensive nested groups search before exhausting all AuthLDAPGroupAttribute checks on the current group. PR 52464 [Eric Covener]

*) mod_lua: Add new directive LuaAuthzProvider to allow implementing an authorization provider in lua. [Stefan Fritsch]

*) core: Be less strict when checking whether Content-Type is set to "application/x-www-form-urlencoded" when parsing POST data, or we risk losing data with an appended charset. PR 53698 [Petter Berntsen < petterb gmail.com>]

*) httpd.conf: Added configuration directives to set a bad_DNT environment variable based on User-Agent and to remove the DNT header field from incoming requests when a match occurs. This currently has the effect of removing DNT from requests by MSIE 10.0 because it deliberately violates the current specification of DNT semantics for HTTP. [Roy T. Fielding]

*) mod_socache_shmcb: Fix bus error due to a misalignment in some 32 bit builds, especially on Solaris Sparc. PR 53040. [Rainer Jung]

*) mod_cache: Set content type in case we return stale content. [Ruediger Pluem]

*) Windows: Fix SSL failures on windows with AcceptFilter https none. PR 52476. [Jeff Trawick]

*) ab: Fix read failure when targeting SSL server. [Jeff Trawick]

*) The following now respect DefaultRuntimeDir/DEFAULT_REL_RUNTIMEDIR: - mod_auth_digest: shared memory file [Jeff Trawick]

*) htpasswd: Use correct file mode for checking if file is writable. PR 45923. [Stefan Fritsch]

*) mod_rewrite: Fix crash with dbd RewriteMaps. PR 53663. [Mikhail T. < mi apache aldan algebra com>]

*) mod_ssl: Add new directive SSLCompression to disable TLS-level compression. PR 53219. [BjÃ¶rn Jacke < bjoern j3e de>, Stefan Fritsch]

*) mod_lua: Add a few missing request_rec fields. Rename remote_ip to client_ip to match conn_rec. [Stefan Fritsch]

*) mod_lua: Change prototype of vm_construct, to work around gcc bug which causes a segfault. PR 52779. [Dick Snippe < Dick Snippe tech omroep nl>]

*) mpm_event: Don't count connections in lingering close state when calculating how many additional connections may be accepted. [Stefan Fritsch]

*) mod_ssl: If exiting during initialization because of a fatal error, log a message to the main error log pointing to the appropriate virtual host error log. [Stefan Fritsch]

*) mod_proxy_ajp: Reduce memory usage in case of many keep-alive requests on one connection. PR 52275. [Naohiro Ooiwa < naohiro ooiwa miraclelinux com>]

*) mod_proxy_balancer: Restore balancing after a failed worker has recovered when using lbmethod_bybusyness. PR 48735. [Jeff Trawick]

*) mod_setenvif: Compile some global regex only once during startup. This should save some memory, especially with .htaccess. [Stefan Fritsch]

*) core: Add the port number to the vhost's name in the scoreboard. [Stefan Fritsch]

*) mod_proxy: Fix ProxyPassReverse for balancer configurations. PR 45434. [Joe Orton]

*) mod_lua: Add the parsebody function for parsing POST data. PR 53064. [Daniel Gruno]

*) apxs: Use LDFLAGS from config_vars.mk in addition to CFLAGS and CPPFLAGS. [Stefan Fritsch]

*) mod_proxy: Fix memory leak or possible corruption in ProxyBlock implementation. [Ruediger Pluem, Joe Orton]

) mod_proxy: Check hostname from request URI against ProxyBlock list, not forward proxy, if ProxyRemote is configured. [Joe Orton]

) mod_proxy_connect: Avoid DNS lookup on hostname from request URI if ProxyRemote is configured. PR 43697. [Joe Orton]

*) mpm_event, mpm_worker: Remain active amidst prevalent child process resource shortages. [Jeff Trawick]

*) Add "strict" and "warnings" pragmas to Perl scripts. [Rich Bowen]

*) The following now respect DefaultRuntimeDir/DEFAULT_REL_RUNTIMEDIR: - core: the scoreboard (ScoreBoardFile), pid file (PidFile), and mutexes (Mutex) [Jim Jagielski]

*) ab: Fix bind() errors. [Joe Orton]

*) mpm_event: Don't do a blocking write when starting a lingering close from the listener thread. PR 52229. [Stefan Fritsch]

*) mod_so: If a filename without slashes is specified for LoadFile or LoadModule and the file cannot be found in the server root directory, try to use the standard dlopen() search path. [Stefan Fritsch]

*) mpm_event, mpm_worker: Fix cases where the spawn rate wasn't reduced after child process resource shortages. [Jeff Trawick]

*) mpm_prefork: Reduce spawn rate after a child process exits due to unexpected poll or accept failure. [Jeff Trawick]

*) core: Log value of Status header line in script responses rather than the fixed header name. [Chris Darroch]

*) mpm_ssl: Fix handling of empty response from OCSP server. [Jim Meyering < meyering redhat.com>, Joe Orton]

*) mpm_event: Fix handling of MaxConnectionsPerChild. [Stefan Fritsch]

*) mod_authz_core: If an expression in "Require expr" returns denied and references %{REMOTE_USER}, trigger authentication and retry. PR 52892. [Stefan Fritsch]

*) core: Always log if LimitRequestFieldSize triggers. [Stefan Fritsch]

*) mod_deflate: Skip compression if compression is enabled at SSL level. [Stefan Fritsch]

*) core: Add missing HTTP status codes registered with IANA. [Julian Reschke < julian.reschke gmx.de>, Rainer Jung]

*) mod_ldap: Treat the "server unavailable" condition as a transient error with all LDAP SDKs. [Filip Valder < filip.valder vsb.cz>]

*) core: Fix spurious "not allowed here" error returned when the Options directive is used in .htaccess and "AllowOverride Options" (with no specific options restricted) is configured. PR 53444. [Eric Covener]

*) mod_authz_core: Fix parsing of Require arguments in < AuthzProviderAlias>. PR 53048. [Stefan Fritsch]

*) mod_log_config: Fix %{abc}C truncating cookie values at first "=". PR 53104. [Greg Ames]

*) mod_ext_filter: Fix error_log spam when input filters are configured.
[Joe Orton]

*) mod_rewrite: Add "AllowAnyURI" option. PR 52774. [Joe Orton]

*) htdbm, htpasswd: Don't crash if crypt() fails (e.g. with FIPS enabled). [Paul Wouters < pwouters redhat.com>, Joe Orton]

*) core: Use a TLS 1.0 close_notify alert for internal dummy connection if the chosen listener is configured for https. [Joe Orton]

*) mod_proxy: Use the the same hostname for SNI as for the HTTP request when forwarding to SSL backends. PR 53134. [Michael Weiser < michael weiser.dinsnail.net>, Ruediger Pluem]

*) mod_info: Display all registered providers. [Stefan Fritsch]

*) mod_ssl: Send the error message for speaking http to an https port using HTTP/1.0 instead of HTTP/0.9, and omit the link that may be wrong when using SNI. PR 50823. [Stefan Fritsch]

*) core: Fix segfault in logging if r->useragent_addr or c->client_addr is unset. PR 53265. [Stefan Fritsch]

*) log_server_status: Bring Perl style forward to the present, use standard modules, update for new format of server-status output. PR 45424. [Richard Bowen, Dave Brondsema, and others]

*) mod_sed, mod_log_debug, mod_rewrite: Symbol namespace cleanups. [Joe Orton, AndrÃ© Malo]

*) core: Prevent "httpd -k restart" from killing server in presence of config error. [Joe Orton]

*) mod_proxy_fcgi: If there is an error reading the headers from the backend, send an error to the client. PR 52879. [Stefan Fritsch] 13-May-2012 Changes with Apache 2.4.2 Apache Lounge change:

*) Upgraded zlib to 1.2.7 (Changelog)

*) Upgraded OpenSSL to 1.0.1c and 0.9.8x (Changelog) 20-April-2012 Changes with Apache 2.4.2 Apache Lounge change:

*) Upgraded OpenSSL from 1.0.1 to 1.0.1a (Changelog) 6-April-2012 Changes with Apache 2.4.2 Apache Lounge changes:

*) Crypto enabled from now on

*) Include manual files from now on

*) Win64 Binary apr-1.4.6 patched (ASF PR: 49155) WIN64 wasn't defined correctly in APR, resulting in crashes.

*) PCRE upgraded from 8.21 to 8.30 (Changelog)

*) OpenSSL upgraded from 1.0.0g to 1.0.1 (Changelog)

*) Expat upgraded from 1.95.7 to 2.1.0 (Changelog) Solves a few security vulnerabilities

*) Lua upgraded from 5.1.4 to 5.1.5 (Changelog)

*) For a SSL issue, see Apache 2.4.2 available

ASF changes:

*) SECURITY: CVE-2012-0883 (cve.mitre.org) envvars: Fix insecure handling of LD_LIBRARY_PATH that could lead to the current working directory to be searched for DSOs. [Stefan Fritsch]

*) mod_slotmem_shm: Honor DefaultRuntimeDir [Jim Jagielski]

*) mod_ssl: Fix crash with threaded MPMs due to < race condition when initializing EC temporary keys. [Stefan Fritsch]

*) mod_proxy: Add the forcerecovery balancer parameter that determines if recovery for balancer workers is enforced. [Ruediger Pluem]

*) Fix MPM DSO load failure on AIX. [Jeff Trawick]

*) mod_proxy: Correctly set up reverse proxy worker. PR 52935. [Petter Berntsen < petterb gmail.com>]

*) mod_sed: Don't define PATH_MAX to a potentially undefined value, causing compile problems on GNU hurd. [Stefan Fritsch]

*) core: Add ap_runtime_dir_relative() and DefaultRuntimeDir. [Jeff Trawick]

*) core: Fix breakage of Listen directives with MPMs that use a per-directory config. PR 52904. [Stefan Fritsch]

*) core: Disallow directives in AllowOverrideList which are only allowed in VirtualHost or server context. These are usually not prepared to be called in .htaccess files. [Stefan Fritsch]

*) core: In AllowOverrideList, do not allow 'None' together with other directives. PR 52823. [Stefan Fritsch]

*) mod_slotmem_shm: Support DEFAULT_REL_RUNTIMEDIR for file-based shm. [Jim Jagielski]

*) core: Fix merging of AllowOverrideList and ContentDigest. [Stefan Fritsch]

*) mod_request: Fix validation of the KeptBodySize argument so it doesn't always throw a configuration error. PR 52981 [Eric Covener]

*) core: Add filesystem paths to access denied / access failed messages AH00035 and AH00036. [Eric Covener]

*) mod_dumpio: Properly handle errors from subsequent input filters. PR 52914. [Stefan Fritsch]

*) Unix MPMs: Fix small memory leak in parent process if connect() failed when waking up children. [Joe Orton]

*) "DirectoryIndex disabled" now undoes DirectoryIndex settings in the current configuration section, not just previous config sections. PR 52845. [Eric Covener]

*) mod_xml2enc: Fix broken handling of EOS buckets which could lead to response headers not being sent. PR 52766. [Stefan Fritsch]

*) mod_ssl: Properly free the GENERAL_NAMEs. PR 32652. [Kaspar Brand]

*) core: Check during config test that directories for the access logs actually exist. PR 29941. [Stefan Fritsch]

*) mod_xml2enc, mod_proxy_html: Enable per-module loglevels. [Stefan Fritsch]

*) mod_filter: Fix segfault with AddOutputFilterByType. PR 52755. [Stefan Fritsch]

*) mod_session: Sessions are encoded as application/x-www-form-urlencoded strings, however we do not handle the encoding of spaces properly. Fixed. [Graham Leggett]

*) Configuration: Example in comment should use a path consistent with the default configuration. PR 52715. [Rich Bowen, Jens Schleusener, Rainer Jung]

*) Configuration: Switch documentation links from trunk to 2.4. [Rainer Jung]

*) configure: Fix out of tree build using apr and apr-util in srclib. [Rainer Jung] 6-March-2012 Changes with Apache 2.4.1 *) Build with VC10

*) Win64 apr-1.4.6 patched (ASF PR: 49155) WIN64 wasn't defined correct, resulting in crashes. Now using _WIN64 instead of WIN64 (compiler define vs. SDK define) in .c/.h. 15-Febuary-2012 Changes with Apache 2.4.1 *) Upgraded OpenSSL from 1.0.0e to 1.0.0g (Changelog)

*) Build OpenSSL with nasm 2.09.10 (was 2.05.01), see nasm home

*) Upgraded zlib from 1.2.5 to 1.2.6 (Changelog)

*) Upgraded APR from 1.4.5 to 1.4.6 (Changelog)

*) SECURITY: CVE-2012-0053 (cve.mitre.org) Fix an issue in error responses that < could expose "httpOnly" cookies when no custom ErrorDocument is specified for status code 400.
[Eric Covener]

*) mod_proxy_balancer: Fix crash on Windows. PR 52402 [Mladen Turk]

*) core: Check during configtest that the directories for error logs exist. PR 29941 [Stefan Fritsch]

*) Core configuration: add AllowOverride option to treat syntax errors in .htaccess as non-fatal. PR 52439 [Nick Kew, Jim Jagielski]

*) core: Fix memory consumption in core output filter with streaming bucket types like CGI or PIPE. [Joe Orton, Stefan Fritsch]

*) configure: Disable modules at configure time if a prerequisite module is not enabled. PR 52487. [Stefan Fritsch]

*) Rewrite and proxy now decline what they don't support rather than fail the request. [Joe Orton]

*) Fix building against external apr plus ap-util if apr is not installed in a system default path. [Rainer Jung]

*) Doxygen fixes and improvements. [Joe Orton, Igor Gali?]

*) core: Fix building against PCRE 8.30 by switching from the obsolete pcre_info() to pcre_fullinfo(). PR 52623 [Ruediger Pluem, Rainer Jung] 17-January-2012 Changes with Apache 2.4.0 *) SECURITY (CVE-2012-0031): Fix scoreboard issue which could allow an unprivileged child process could cause the parent to crash at shutdown rather than terminate cleanly. [Joe Orton]

*) mod_ssl: Fix compilation with xlc on AIX. PR 52394. [Stefan Fritsch]

*) mod_log_config: Fix segfault when trying t< o log a nameless, valueless cookie. PR 52256. [Rainer Canavan < rainer-apache 7val com>]

*) mod_ssl: when compiled against OpenSSL 1.0.1 or later, allow explicit control of TLSv1.1 and TLSv1.2 through the SSLProtocol directive. [Kaspar Brand]

*) mod_ssl: set OPENSSL_NO_SSL_INTERN when compiling against OpenSSL 1.0.1 or later, to improve binary compatibility with future OpenSSL releases. [Kaspar Brand]

*) mod_mime: Don't arbitrarily bypass AddOutputFilter during a ProxyPass, but then allow AddOutputFilter during a RewriteRule [P]. Make mod_mime behave identically in both cases. PR52342. [Graham Leggett]

*) Move ab, logresolve, httxt2dbm and apxs to bin from sbin, along with corresponding man pages. [Graham Leggett]

*) Distinguish properly between the bindir and sbindir directories when installing binaries. Previously all binaries were silently installed to sbindir, whether they were system administration commands or not. [Graham Leggett]


#CHANGE LOG TOMCAT

Changelog

Tomcat 8.0.41 (violetagg)

Cluster

Add: Make the accessTimeout configurable in BackupManager. The accessTimeout is used as a timeout period for PING in replication map. (kfujino) Web applications

Fix: Ensure the ASF logo image is displayed in host-manager. (violetagg) not released Tomcat 8.0.40 (violetagg)

Catalina

Add: 53602: Add HTTP status code 451 (RFC 7725) to the list of HTTP status codes recognised by Tomcat. (markt) Fix: 60446: Handle the case where the stored user credential uses a different key length than the length currently configured for the CredentialHandler. Based on a patch by Niklas Holm. (markt) Fix: 60351: Delay creating META-INF/war-tracker file until after the WAR has been expanded to address the case where the Tomcat process terminates during the expansion. (markt) Fix: Correctly handle the configClass attribute of a Host when embedding Tomcat. (markt) Fix: 60379: Dispose of the GSS credential once it is no longer required. Patch provided by Michael Osipov. (markt) Fix: 60380: Ensure that a call to HttpServletRequest#logout() triggers a call to TomcatPrincipal#logout(). Based on a patch by Michael Osipov. (markt) Fix: 60387: Correct the javadoc for o.a.catalina.AccessLog.setRequestAttributesEnabled. The default value is different for the different implementations. (violetagg) Code: 60393: Use consistent parameter naming in implementations of Realm#authenticate(GSSContext, boolean). (markt) Fix: 60395: Log when an Authenticator passes an incomplete GSSContext to a Realm since it indicates a bug in the Authenticator. Patch provided by Michael Osipov. (markt) Fix: Correctly generate URLs for resources located inside JARs that are themselves located inside a packed WAR file. (markt) Fix: 60410: Ensure that multiple calls to JarInputStreamWrapper#close() do not incorrectly trigger the closure of the underlying JAR or WAR file. (markt) Fix: 60411: Implement support in the RewriteValve for symbolic names to specify the redirect code to use when returning a redirect response to the user agent. Patch provided by Michael Osipov. (markt) Fix: 60413: In the RewriteValve write empty capture groups as the empty string rather than as "null" when generating the re-written URL. Based on a patch by Michael Osipov. (markt) Update: Update the warnings that reference required options for running on Java 9 to use the latest syntax for those options. (markt) Fix: 60513: Fix thread safety issue with RMI cleanup code. (remm) Coyote

Fix: Ensure that the endpoint is able to unlock the acceptor thread during shutdown if the endpoint is configured to listen to any local address of a specific type such as 0.0.0.0 or ::. (markt) Fix: Prevent read time out when the file is deleted while serving the response. The issue was observed only with APR Connector and sendfile enabled. (violetagg) Fix: Improve the logic that selects an address to use to unlock the Acceptor to take account of platforms what do not listen on all local addresses when configured with an address of 0.0.0.0 or ::. (markt) Fix: 60409: When unable to complete sendfile request, ensure the Processor will be added to the cache only once. (markt/violetagg) Jasper

Fix: 60431: Improve handling of varargs in UEL expressions. Based on a patch by Ben Wolfe. (markt) Fix: 60497: Restore previous tag reuse behavior following the use of try/finally. (remm) Fix: Improve the error handling for simple tags to ensure that the tag is released and destroyed once used. (remm) Fix: 60497: Follow up fix using a better variable name for the tag reuse flag. (remm) Fix: Revert use of try/finally for simple tags. (remm) Web applications

Fix: Correct a typo in Host Configuration Reference. Issue reported via comments.apache.org. (violetagg) Fix: 60344: Add a note to BUILDING.txt regarding using the source bundle with the correct line endings. (markt) Fix: 60412: Add information on the comment syntax for the RewriteValve configuration. (markt) Fix: 60467: remove problematic characters from XML documentation. Based upon a patch by Michael Osipov. (schultz) Add: In the documentation web application, be explicit that clustering requires a secure network for all of the cluster network traffic. (markt) Update: Update the ASF logos to the new versions. Fix: 60468: Correct the format of the sample ISO-8601 date used to report the build date for the documentation. Patch provided by Michael Osipov. (markt) Tribes

Fix: Reduce the warning logs for a message received from a different domain in order to avoid excessive log outputs. (kfujino) Add: Add log message that PING message has received beyond the timeout period. (kfujino) Fix: When a PING message that beyond the time-out period has been received, make sure that valid member is added to the map membership. (kfujino) WebSocket

Fix: 60437: Avoid possible handshake overflows in the websocket client. (remm) jdbc-pool

Add: 58816: Implement the statistics of jdbc-pool. The stats infos are borrowedCount, returnedCount, createdCount, releasedCount, reconnectedCount, releasedIdleCount and removeAbandonedCount. (kfujino) Fix: 60194: If validationQuery is not specified, connection validation is done by calling the isValid() method. (kfujino) Fix: 60398: Fix testcase of TestSlowQueryReport. (kfujino) Add: Enable reset the statistics without restarting the pool. (kfujino) Other

Fix: 60366: Change catalina.bat to use directly LOGGING_MANAGER and LOGGING_CONFIG variables in order to configure logging, instead of modifying JAVA_OPTS. Patch provided by Petter Isberg. (violetagg) Add: New property is added test.verbose in order to control whether the output of the tests is displayed on the console or not. Patch provided by Emmanuel Bourg. (violetagg) Update: Update the ASF logos used in the Apache Tomcat installer for Windows to use the new versions. Fix: Spelling corrections provided by Josh Soref. (violetagg) 2016-11-14 Tomcat 8.0.39 (violetagg)

Catalina

Fix: When creating a new Connector via JMX, ensure that both HTTP/1.1 and AJP/1.3 connectors can be created. (markt) Fix: Include the Context name in the log message when an item cannot be added to the cache. (markt) Fix: Exclude JAR files in /WEB-INF/lib from the static resource cache. (markt) Fix: When calling getResourceAsStream() on a directory, ensure that null is returned. (markt) Fix: 60161: Allow creating subcategories of the container logger, and use it for the rewrite valve. (remm) Fix: Correctly test for control characters when reading the provided shutdown password. (markt) Fix: When configuring the JMX remote listener, specify the allowed types for the credentials. (markt) Coyote

Fix: Correct the HTTP header parser so that DEL is not treated as a valid token character. (markt) Fix: 60319: When using an Executor, disconnect it from the Connector attributes maxThreads, minSpareThreads and threadPriority to enable the configuration settings to be consistently reported. These Connector attributes will be reported as -1 when an Executor is in use. The values used by the executor may be set and obtained via the Executor. (markt) Fix: If an I/O error occurs during async processing on a non-container thread, ensure that the onError() event is triggered. (markt) Fix: Improve detection of I/O errors during async processing on non-container threads and trigger async error handling when they are detected. (markt) Add: Add additional checks for valid characters to the HTTP request line parsing so invalid request lines are rejected sooner. (markt) Web applications

Fix: Correct a typo in HTTP Connector How-To. Issue reported via comments.apache.org. (violetagg) Fix: Fix default value of validationInterval attribute in jdbc-pool. (kfujino) Fix: Correct a typo in CGI How-To. Issue reported via comments.apache.org. (violetagg) Tribes

Fix: When the proxy node sends a backup retrieve message, ensure that using the channelSendOptions that has been set rather than the default channelSendOptions. (kfujino) Other

Update: Update the ECJ compiler to version 4.5.1. (markt) Fix: Remove classes from tomcat-util-scan.jar that are duplicates of those in tomcat-util.jar. (markt) 2016-10-10 Tomcat 8.0.38 (markt)

Catalina

Add: 59961: Add an option to the StandardJarScanner to control whether or not JAR Manifests are scanned for additional class path entries. (markt) Fix: 60013: Refactor the previous fix to align the behaviour of the Rewrite Valve with mod_rewrite. As part of this, provide an implementation for the B and NE flags and improve the handling for the QSA flag. Includes multiple test cases by Santhana Preethiand a patch by Tiago Oliveira. (markt) Fix: 60087: Refactor the web resources handling to use the Tomcat specific war:file:... URL protocol to refer to WAR files and their contents rather than the standard jar:file:... form since some components of the JRE, such as JAR verification, give unexpected results when the standard form is used. A side-effect of the refactoring is that when using packed WARs, it is now possible to reference a WAR and/or specific JARs within a WAR in the security policy file used when running under a SecurityManager. (markt) Fix: 60116: Fix a problem with the rewrite valve that caused back references evaluated in conditions to be forced to lower case when using the NC flag. (markt) Fix: Ensure Digester.useContextClassLoader is considered in case the class loader is used. (violetagg) Fix: 60117: Ensure that the name of LogLevel is localized when using OneLineFormatter. Patch provided by Tatsuya Bessho. (kfujino) Fix: 60146: Improve performance for resource retrieval by making calls to WebResource.getInputStream() trigger caching if the resource is small enough. Patch provided by mohitchugh. (markt) Add: 60151: Improve the exception error messages when a ResourceLink fails to specify the type, specifies an unknown type or specifies the wrong type. (markt) Fix: 60167: Ignore empty lines in /etc/passwd files when using the PasswdUserDatabase. (markt) Fix: 60170: Exclude the compressed test file index.html.br from RAT analysis. Patch provided by Gavin McDonald. (markt) Fix: When starting web resources, ensure that class resources are only started once. (markt) Fix: Improve the access checks for linked global resources to handle the case where the current class loader is a child of the web application class loader. (markt) Fix: 60199: Log a warning if deserialization issues prevent a session attribute from being loaded. (markt) Coyote

Fix: Correctly handle a call to AsyncContext.complete() from a non-container thread when non-blocking I/O is being used. (markt) Add: Refactor the code that implements the requirement that a call to complete() or dispatch() made from a non-container thread before the container initiated thread that called startAsync() completes must be delayed until the container initiated thread has completed. Rather than implementing this by blocking the non-container thread, extend the internal state machine to track this. This removes the possibility that blocking the non-container thread could trigger a deadlock. (markt) Fix: 60123: Avoid potential threading issues that could cause excessively large vales to be returned for the processing time of a current request. (markt) Fix: 60174: Log instances of HeadersTooLargeException during request processing. (markt) Jasper

Fix: 60101: Remove preloading of the class that was deleted. (violetagg) Web applications

Add: Expand the documentation for the nested elements within a Resources element to clarify the behaviour of different configuration options with respect to the order in which resources are searched. (markt) Add: Add an example of using the classesToInitialize attribute of the JreMemoryLeakPreventionListener to the documentation web application. Based on a patch by Cris Berneburg. (markt) Fix: 60192: Correct a typo in the status output of the Manager application. Patch provided by Radhakrishna Pemmasani. (markt) jdbc-pool

Fix: Notify jmx when returning the connection that has been marked suspect. (kfujino) Fix: Ensure that the POOL_EMPTY notification has been added to the jmx notification types. (kfujino) Fix: 60099: Ensure that use all method arguments as a cache key when using StatementCache. (kfujino) Fix: 60139: Correct Javadocs for PoolConfiguration.getValidationInterval and setValidationInterval. Reported by Phillip Webb. (kfujino) Other

Fix: Update the download location for Objenesis. (violetagg) Fix: 60164: Replace log4j-core.jar with log4j-web.jar since it is log4j-web*.jar that contains the ServletContainerInitializer. (markt) Add: Add documentation to the bin/catalina.bat script to remind users that environment variables don't affect the configuration of Tomcat when run as a Windows Service. Based upon a documentation patch by James H.H. Lampert. (schultz) Update: Update the packaged version of the Tomcat Native Library to 1.2.10 to pick up the latest Windows binaries built with OpenSSL 1.0.2j. (markt) 2016-09-05 Tomcat 8.0.37 (markt)

Catalina

Fix: 57705: Add debug logging for requests denied by the remote host and remote address valves and filters. Based on a patch by Graham Leggett. (markt) Add: 59399: Add a new option to the Realm implementations that ship with Tomcat that allows the HTTP status code used for HTTP -> HTTPS redirects to be controlled per Realm. (markt) Update: Change the default of the sessionCookiePathUsesTrailingSlash attribute of the Context element to false since the problems caused when a Servlet is mapped to /* are more significant than the security risk of not enabling this option by default. (markt) Fix: Do not attempt to start web resources during a web application's initialisation phase since the web application is not fully configured at that point and the web resources may not be correctly configured. (markt) Fix: 59708: Modify the LockOutRealm logic. Valid authentication attempts during the lock out period will no longer reset the lock out timer to zero. (markt) Fix: Improve error handling around user code prior to calling InstanceManager.destroy() to ensure that the method is executed. (markt) Fix: 59813: Ensure that circular relations of the Class-Path attribute from JAR manifests will be processed correctly. (violetagg) Fix: Ensure that reading the singleThreadModel attribute of a StandardWrapper via JMX does not trigger initialisation of the associated servlet. With some frameworks this can trigger an unexpected initialisation thread and if initialisation is not thread-safe the initialisation can then fail. (markt) Fix: Compatibility with rewrite from httpd for non existing headers. (jfclere) Fix: By default, treat paths used to obtain a request dispatcher as encoded. This behaviour can be changed per web application via the dispatchersUseEncodedPaths attribute of the Context. (markt) Fix: 59839: Apply roleSearchAsUser to all nested searches in JNDIRealm. (fschumacher) Fix: 59859: Fix resource leak in WebDAV servlet. Based on patch by Coty Sutherland. (fschumacher) Add: Provide a mechanism that enables the container to check if a component (typically a web application) has been granted a given permission when running under a SecurityManager without the current execution stack having to have passed through the component. Use this new mechanism to extend SecurityManager protection to the system property replacement feature of the digester. (markt) Add: When retrieving an object via a ResourceLink, ensure that the object obtained is of the expected type. (markt) Fix: 59824: Mark the RewriteValve as supporting async processing by default. (markt) Fix: 59862: Allow nested jar files scanning to be filtered with the system property tomcat.util.scan.StandardJarScanFilter.jarsToSkip. Patch is provided by Terence Bandoian. (violetagg) Fix: 59866: When scanning WEB-INF/classes for annotations, don't scan the contents of WEB-INF/classes/META-INF (if present) since classes will never be loaded from that location. (markt) Fix: 59888: Correctly handle tabs and spaces in quoted version one cookies when using the Rfc6265CookieProcessor. (markt) Fix: 59912: Fix an edge case in input stream handling where an IOException could be thrown when reading a POST body. (markt) Fix: 59960: Fix Javadoc so it builds with Java 8. Patch by Coty Sutherland. (markt) Fix: 59966: Do not start the web application if the error page configuration in web.xml is invalid. (markt) Fix: Switch the CGI servlet to the standard logging mechanism and remove support for the debug attribute. (markt) Fix: Changes to the allowLinking attribute of a StandardRoot instance now invalidate the cache if caching is enabled. (markt) Add: Add a new initialisation parameter, envHttpHeaders, to the CGI Servlet to mitigate httpoxy (CVE-2016-5388) by default and to provide a mechanism that can be used to mitigate any future, similar issues. (markt) Add: When adding and removing ResourceLinks dynamically, ensure that the global resource is only visible via the ResourceLinkFactory when it is meant to be. (markt) Fix: 60008: When processing CORs requests, treat any origin with a URI scheme of file as a valid origin. (markt) Fix: Improve handling of exceptions during a Lifecycle events triggered by a state transition. The exception is now caught and the component is now placed into the FAILED state. (markt) Fix: 60013: Fix encoding issues when using the RewriteValve with UTF-8 query strings or UTF-8 redirect URLs. (markt) Fix: 60022: Improve handling when a WAR file and/or the associated exploded directory are symlinked into the appBase. (markt) Fix: Fix a file descriptor leak when reading the global web.xml. (markt) Fix: Consistently decode URL patterns provided via web.xml using the encoding of the web.xml file where specified or UTF-8 where no explicit encoding is specified. (markt) Fix: Make timing attacks against the Realm implementations harder. (schultz) Coyote

Fix: Improve error handling around user code prior to calling InstanceManager.destroy() to ensure that the method is executed. (markt) Fix: Extend synchronization for NIO2 writes to avoid ConcurrentModificationException observed during testing. (markt) Fix: 59904: Add a limit (default 200) for the number of cookies allowed per request. Based on a patch by gehui. (markt) Fix: 59925: Correct regression in r1628368 and ensure that HTTP separators are handled as configured in the LegacyCookieProcessor. Patch provided by Kyohei Nakamura. (markt) Fix: OpenSSL now disables 3DES by default so reflect this when using OpenSSL syntax to select ciphers. (markt) Jasper

Fix: Improve error handling around user code prior to calling InstanceManager.destroy() to ensure that the method is executed. (markt) Fix: Improve the error handling for custom tags to ensure that the tag is returned to the pool or released and destroyed once used. (markt) Fix: 60032: Fix handling of method calls that use varargs within EL value expressions. (markt) Fix: Ignore engineOptionsClass and scratchdir when running under a security manager. (markt) Fix: Fixed StringIndexOutOfBoundsException. Based on a patch provided by wuwen via Github. (violetagg) WebSocket

Fix: Improve error handling around user code prior to calling InstanceManager.destroy() to ensure that the method is executed. (markt) Fix: 59908: Ensure that a reason phrase is included in the close message if a session is closed due to a timeout. (markt) Web Applications

Fix: Do not log an additional case of IOExceptions in the error handler for the Drawboard WebSocket example when the root cause is the client disconnecting since the logs add no value. (markt) Fix: 59642: Mention the localDataSource in the DataSourceRealm section of the Realm How-To. (markt) Fix: Follow-up to the fix for 59399. Ensure that the new attribute transportGuaranteeRedirectStatus is documented for all Realms. Also document the NullRealm and when it is automatically created for an Engine. (markt) Fix: Fix the description of maxAge attribute in jdbc-pool doc. This attribute works both when a connection is returned and when a connection is borrowed. (kfujino) Fix: 59774: Correct the prefix values in the documented examples for configuring the AccessLogValve. Patch provided by Mike Noordermeer. (markt) Fix: 59868: Clarify the documentation for the Manager web application to make clearer that the host name and IP address in the server section are the primary host name and IP address. (markt) Fix: MBeans Descriptors How-To is moved to mbeans-descriptors-howto.html. Patch provided by Radoslav Husar. (violetagg) Fix: Update NIO Connector configuration documentation with an information about socket.directSslBuffer. (violetagg) Fix: 60034: Correct a typo in the Manager How-To page of the documentation web application. (markt) Tribes

Add: Add log message when the ping has timed-out. (kfujino) Fix: If the ping message has been received at the AbstractReplicatedMap#leftOver method, ensure that notify the member is alive than ignore it. (kfujino) jdbc-pool

Fix: Fix the duplicated connection release when connection verification failed. (kfujino) Fix: Ensure that do not remove the abandoned connection that has been already released. (kfujino) Fix: In order to avoid the unintended skip of PoolCleaner, remove the check code of the execution interval in the task that has been scheduled. (kfujino) Fix: 59850: Ensure that the ResultSet is closed when enabling the StatementCache interceptor. (kfujino) Fix: 59923: Reduce the default value of validationInterval in order to avoid the potential issue that continues to return an invalid connection after database restart. (kfujino) Fix: Ensure that the ResultSet is returned as Proxy object when enabling the StatementDecoratorInterceptor. (kfujino) Fix: 60043: Ensure that the suspectTimeout works without removing connection when the removeAbandoned is disabled. (kfujino) Fix: Add log message of when returning the connection that has been marked suspect. (kfujino) Fix: Correct Javadoc for ConnectionPool.suspect(). Based on a patch by Yahya Cahyadi. (markt) Other

Update: 59276: Update optional Checkstyle library to 6.17. (kkolinko) Add: Use the mirror network rather than the ASF master site to download the current ASF dependencies. (markt) Update: Update the packaged version of the Tomcat Native Library to 1.2.8 to pick up the latest fixes and make 1.2.8 the minimum recommended version. (markt) Fix: 59899: Update Tomcat's copy of the Java Persistence annotations to include the changes made in 2.1 / JavaEE 7. (markt) Fix: Fixed typos in mbeans-descriptors.xml files. (violetagg) Update: Update the internal fork of Commons BCEL to r1757132 to align with the BCEL 6 release. (markt) Update: Update the internal fork of Commons DBCP2 to r1757164 to pick up a couple of bug fixes. (markt) Update: Update the internal fork of Commons Codec to r1757174. Code formatting changes only. (markt) Update: Update the internal fork of Commons FileUpload to afdedc9. This pulls in a fix to improve the performance with large multipart boundaries. (markt) 2016-06-13 Tomcat 8.0.36 (markt)

Catalina

Fix: RMI Target related memory leaks are avoidable which makes them an application bug that needs to be fixed rather than a JRE bug to work around. Therefore, start logging RMI Target related memory leaks on web application stop. Add an option that controls if the check for these leaks is made. Log a warning if running on Java 9 with this check enabled but without the command line option it requires. (markt) Fix: Ensure NPE will not be thrown during deployment when scanning jar files without MANIFEST.MF file. (violetagg) Fix: 59604: Correct the assumption made in the URL decoding that the default platform encoding is always compatible with ISO-8859-1. This assumption is not always valid, e.g. on z/OS. (markt) Fix: 59608: Skip over any invalid Class-Path attribute from JAR manifests. Log errors at debug level due to many bad libraries. (remm) Fix: Fix error message when failed to register MBean. (kfujino) Coyote

Fix: Ensure that requests with HTTP method names that are not tokens (as required by RFC 7231) are rejected with a 400 response. (markt) Fix: When an asynchronous request is processed by the AJP connector, ensure that request processing has fully completed before starting the next request. (markt) Fix: If an async dispatch results in the completion of request processing, ensure that any remaining request body is swallowed before starting the processing of the next request else the remaining body may be read as the start of the next request leading to a 400 response. (markt) Jasper

Fix: 59567: Fix NPE scanning webapps for TLDs when an exploded JAR has an empty WEB-INF/classes/META-INF folder. (remm) Fix: Fix a memory leak in the expression language implementation that caused the class loader of the first web application to use expressions to be pinned in memory. (markt) Fix: 59640: NPEs with not found TLDs. (remm) Fix: 59654: Improve error message when attempting to use a TLD file from an invalid location. Patch provided by Huxing Zhang. (markt) Web applications

Fix: 58891: Update the SSL how-to. Based on a suggestion by Alexander Kjäll. (markt) jdbc-pool

Fix: Fix a memory leak with the pool cleaner thread that retained a reference to the web application class loader for the first web application to use a connection pool. (markt) Other

Update: Update the internal fork of Commons DBCP 2 to r1743696 (2.1.1 plus additional fixes). (markt) Update: Update the internal fork of Commons Pool 2 to r1743697 (2.4.2 plus additional fixes). (markt) Update: Update the internal fork of Commons File Upload to r1743698 (1.3.1 plus additional fixes). (markt) Update: Update the option code coverage tool Cobertura to 2.1.1 so it is easier to compare the change in lines of code between 8.0.x and 9.0.x. (markt) Fix: 58626: Add support for a new environment variable (USE_NOHUP) that causes nohup to be used when starting Tomcat. It is disabled by default except on HP-UX where it is enabled by default since it is required when starting Tomcat at boot on HP-UX. (markt) 2016-05-16 Tomcat 8.0.35 (markt)

Catalina

Fix: Ensure that annotated web components packed in web fragments will be processed when unpackWARs is enabled. (violetagg) not released Tomcat 8.0.34 (markt)

Catalina

Fix: 59206: Ensure NPE will not be thrown by o.a.tomcat.util.file.ConfigFileLoader when catalina.base is not specified. (violetagg) Fix: 59217: Remove duplication in the recycling of the path in o.a.tomcat.util.http.ServerCookie. Patch is provided by Kyohei Nakamura. (violetagg) Fix: 59213: Async dispatches should be based off a wrapped request. (remm) Fix: Ensure that javax.servlet.ServletRequest and javax.servlet.ServletResponse provided during javax.servlet.AsyncListener registration are made available via javax.servlet.AsyncEvent.getSuppliedRequest and javax.servlet.AsyncEvent.getSuppliedResponse (violetagg) Fix: 59219: Ensure AsyncListener.onError() is called if an Exception is thrown during async processing. (markt) Fix: 59220: Ensure that AsyncListener.onComplete() is called if the async request times out and the response is already committed. (markt) Fix: 59226: Process the Class-Path attribute from JAR manifests for JARs on the class path excluding JARs packaged in WEB-INF/lib. (markt) Fix: 59255: Fix possible NPE in mapper. (kkolinko/remm) Fix: 59256: slf4j-taglib*.jar should not be excluded from the standard JAR scanning by default. (violetagg) Fix: Clarify in the log message that specifying both urlPatterns and value attributes in WebServlet and WebFilter annotations is not allowed. (violetagg) Fix: Ensure the exceptions caused by Valves will be available in the log files so that they can be evaluated when o.a.catalina.valves.ErrorReportValve.showReport is disabled. Patch is provided by Svetlin Zarev. (violetagg) Fix: Fix handling of Cluster Receiver in StoreConfig. The bind and host attributes define as TransientAttribute. (kfujino) Fix: 59261: ServletRequest.getAsyncContext() now throws an IllegalStateException as required by the Servlet specification if the request is not in asynchronous mode when called. (markt) Fix: 59269: Correct the implementation of PersistentManagerBase so that minIdleSwap functions as designed and sessions are swapped out to keep the active session count below maxActiveSessions. (markt) Fix: 59247: Preload ResourceEntry as a workaround for security manager issues on some JVMs. (kkolinko/remm) Fix: Correctly configure the base path for a resources directory provided by an expanded JAR file. Patch provided by hengyunabc. (markt) Fix: Ensure that /WEB-INF/classes is never processed as a web fragment. (markt) Fix: 59310: Do not add a Content-Length: 0 header for custom responses to HEAD requests that do not set a Content-Length value. (markt) Add: Make a web application's CredentialHandler available through a context attribute. This allows a web application to use the same algorithm for validating or generating new stored credentials from cleartext ones. (schultz) Fix: When normalizing paths, improve the handling when paths end with /. or /.. and ensure that input and output are consistent with respect to whether or not they end with /. (markt) Fix: 59317: Ensure that HttpServletRequest.getRequestURI() returns an encoded URI rather than a decoded URI after a dispatch. (markt) Fix: Use the correct URL for the fragment when reporting errors processing a web-fragment.xml file from a JAR located in an unpacked WAR. (markt) Fix: Ensure that JarScanner only uses the explicit call-back to process WEB-INF/classes and only when configured to treat the contents of WEB-INF/classes as a possible exploded JAR. (markt) Code: Remove the java2DDisposerProtection option from the JreMemoryLeakPreventionListener. The leak is fixed in Java 7 onwards and Tomcat 8 requires Java 7 so the option is unnecessary. (markt) Fix: Ensure that the value for the header X-Frame-Options is constructed correctly according to the specification when ALLOW-FROM option is used. (violetagg) Fix: 59449: In ContainerBase, ensure that the process to remove a child container is the reverse of the process to add one. Patch provided by Huxing Zhang. (markt) Coyote

Fix: When running on Java 7, exclude DHE ciphers from the default cipher list for JSSE connectors since they use weak 768 bit DH keys and cannot be configured to use more secure keys. (markt) Add: Add a new environment variable JSSE_OPTS that is intended to be used to pass JVM wide configuration to the JSSE implementation. The default value is -Djdk.tls.ephemeralDHKeySize=2048 which protects against weak Diffie-Hellman keys with Java 8. (markt) Update: Exclude ciphers that use RSA keys from the default cipher list since they do not support forward secrecy. (markt) Fix: 58970: Fix a connection counting bug in the NIO connector that meant some dropped connections were not removed from the current connection count. (markt) Fix: 59289: Do not recycle upgrade processors in unexpected close situations. (remm) Fix: 59295: Use Locale.toLanguageTag() to construct the Content-Language HTTP header to ensure the locale is correctly represented. Patch provided by zikfat. (markt) Fix: 59451: Correct Javadoc for MessageBytes. Patch provided by Kyohei Nakamura. (markt) Fix: 59450: Correctly handle the case where the LegacyCookieProcessor is configured with allowHttpSepsInV0 set to false and forwardSlashIsSeparator set to true. Patch provided by Kyohei Nakamura. (markt) Jasper

Fix: When scanning JARs for TLDs, correctly handle the (rare) case where a JAR has been exploded into WEB-INF/classes and the web application is deployed as a packed WAR. (markt) WebSocket

Fix: Ensure that a client disconnection triggers the error handling for the associated WebSocket end point. (markt) Add: Make WebSocket client more robust when handling errors during the close of a WebSocket session. (markt) Web applications

Fix: Update in the documentation the link to the maven repository where Tomcat snapshot artifacts are deployed. (markt/violetagg) Fix: Clarify in the documentation that calls to ServletContext.log(String, Throwable) or GenericServlet.log(String, Throwable) are logged at the SEVERE level. (violetagg) Fix: Correct a typo in SSL/TLS Configuration How-To. Issue reported via comments.apache.org. (violetagg) Tribes

Fix: Avoid NPE when a proxy node failed to retrieve a backup entry. (kfujino) Add: Add log of when received an unexpected messages. (kfujino) Add: Add the flag indicating that member is a localMember. (kfujino) Fix: Fix potential NPE that depends on the setting order of attributes of static member when using the static cluster. (kfujino) Add: Add get/set method for the channel that is related to ChannelInterceptorBase. (kfujino) Fix: As with the multicast cluster environment, in the static cluster environment, the local member inherits properties from the cluster receiver. (kfujino) Add: Add get/set method for the channel that is related to each Channel services. (kfujino) Add: Add name to channel in order to identify channels. In tomcat cluster environment, it is set the cluster name + "-Channel" as default value. (kfujino) Add: Add the channel name to the thread which is invoked by channel services in order to identify the associated channel. (kfujino) Fix: Ensure that clear the channel instance from channel services when stopping channel. (kfujino) Add: Implement map state in the replication map. (kfujino) Fix: Ensure that the ping is not executed during the start/stop of the replication map. (kfujino) Fix: In ping processing in the replication map, send not the INIT message but the newly introduced PING message. (kfujino) Other

Fix: 59211: Add hamcrest to Eclipse classpath. Patch is provided by Huxing Zhang. (violetagg) Update: 59280: Update the NSIS Installer used to build the Windows Installers to version 2.51. (kkolinko) Update: Update the packaged version of the Tomcat Native Library to 1.2.7 to pick up the Windows binaries that are based on OpenSSL 1.0.2h and APR 1.5.2. (markt) 2016-03-24 Tomcat 8.0.33 (markt)

Catalina

Fix: Correct a regression in the fix for 58867. When configuring a Context to use an external directory for the docBase, and that directory happens to be located along side the original WAR, use the directory as the docBase rather than expanding the WAR into the appBase and using the newly created expanded directory as the docBase. (markt) Add: 58351: Make the server build date and server version number accessible via JMX. Patch provided by Huxing Zhang. (markt) Add: 58988: Special characters in the substitutions for the RewriteValve can now be quoted with a backslash. (fschumacher) Fix: 58999: Fix class and resource name filtering in WebappClassLoader. It throws a StringIndexOutOfBoundsException if the name is exactly "org" or "javax". (rjung) Code: Remove unnecessary code. There is no support for context level cluster. (kfujino) Add: Make checking for var and map replacement in RewriteValve a bit stricter and correct detection of colon in var replacement. (fschumacher) Fix: Fix the type of InstanceManager attribute of mbean definition of StandardContext. (kfujino) Fix: Refactor the web application class loader to reduce the impact of JAR scanning on the memory footprint of the web application. (markt) Fix: Fix some resource leaks in the error handling for accessing files from JARs and WARs. (markt) Fix: Refactor the JAR and JAR-in-WAR resource handling to reduce the memory footprint of the web application. (markt) Fix: 57809: Deprecate the custom context attribute org.apache.tomcat.util.scan.MergedWebXml which will be removed in Tomcat 9. (markt) Fix: 59001: Correctly handle the case when Tomcat is installed on a path where one of the segments ends in an exclamation mark. (markt) Fix: Expand the fix for 59001 to cover the special sequences used in Tomcat's custom jar:war: URLs. (markt) Fix: 59043: Avoid warning while expiring sessions associated with a single sign on if HttpServletRequest.logout() is used. (markt) Fix: 59054: Ensure that using the CrawlerSessionManagerValve in a distributed environment does not trigger an error when the Valve registers itself in the session. (markt) Fix: Storeconfig handling of alternate cookie processors. (markt/remm) Fix: Storeconfig handling for socket properties. (remm) Add: Log a warning message if a user tries to configure the default session timeout via the deprecated (and ignored) Manager.setMaxInactiveInterval() method. (markt) Fix: Fix incorrect parsing of the NE and NC flags in rewrite rules. (remm) Fix: 59065: Correct the timing of the check for colons in paths on non-Windows systems implemented in catalina.sh so it works correctly with Cygwin. Patch provided by Ed Randall. (markt) Fix: When a Host is configured with an appBase that does not exist, create the appBase before trying to expand an external WAR file into it. (markt) Fix: 59115: When using the Servlet 3.0 file upload, the submitted file name may be provided as a token or a quoted-string. If a quoted-string, unquote the string before returning it to the user. (markt) Fix: 59123: Close NamingEnumeration objects used by the JNDIRealm once they are no longer required. (fschumacher/markt) Fix: 59138: Correct a false positive warning for ThreadLocal related memory leaks when the key class but not the value class has been loaded by the web application class loader. (markt) Fix: 59145: Don't log an invalid warning when a user logs out of a session associated with SSO. (markt) Fix: 59151: Fix a regression in the fix for 56917 that added additional (and arguably unnecessary) validation to the provided redirect location. (markt) Fix: 59154: Fix a NullPointerException in the JASSMemoryLoginModue resulting from the introduction of the CredentialHandler to Realms. (schultz/markt) Coyote

Fix: 58646: Correct a problem with sendfile that resulted in a Processor being added to the cache twice leading to broken responses. (markt) Fix: 59015: Fix potential cause of endless APR Poller loop during shutdown if the Poller experiences an error during the shutdown process. (markt) Fix: Align cipher aliases for kECDHE and ECDHE with the current OpenSSL implementation. (markt) Fix: 59081: Retain the user defined cipher order when defining ciphers using the OpenSSL format. (markt) Fix: 59089: Correctly ignore HTTP headers that include non-token characters in the header name. (markt) Add: Add support for additional OpenSSL cipher aliases from OpenSSL master when specifying ciphers using the OpenSSL syntax. (markt) Jasper

Fix: 57583: Improve the performance of javax.servlet.jsp.el.ScopedAttributeELResolver when resolving attributes that do not exist. This improvement only works when Jasper is used with with Tomcat's EL implementation. (markt) Update: 58111: Update to the Eclipse JDT Compiler 4.5. (markt) Add: Add Java 9 support for JSPs. (markt) WebSocket

Fix: 59014: Ensure that a WebSocket close message can be sent after a close message has been received. (markt) Fix: Correctly handle compression of partial messages when the final message fragment has a zero length payload. (markt) Fix: 59119: Correct read logic for WebSocket client when using secure connections. (markt) Fix: 59134: Correct client connect logic for secure connections made through a proxy. (markt) Fix: 59189: Explicitly release the native memory held by the Inflater and Deflater when using PerMessageDeflate and the WebSocket session ends. Based on a patch by Henrik Olsson. (markt) Web applications

Fix: Correct an error in the documentation of the expected behaviour for automatic deployment. If a WAR is updated and an expanded directory is present, the directory will always be deleted and recreated by expanding the WAR if unpackWARs is true. (markt) Fix: 58935: Remove incorrect references in the documentation to using jar:file: URLs with the Manager application. (markt) Fix: Correct the description of the ServletRequest.getServerPort() in Proxy How-To. Issue reported via comments.apache.org. (violetagg) Fix: Fix a potential indefinite wait in the Comet Chat servlet in the examples web application. (markt) Tribes

Fix: If promoting a proxy node to a primary node when getting a session, notify the change of the new primary node to the original backup node. (kfujino) Other

Fix: 58283: Change the default download location for libraries during the build process from /usr/share/java to ${user.home}/temp. Patch provided by Ahmed Hosni. (markt) Fix: 59031: When using the Windows uninstaller, do not remove the contents of any directories that have been symlinked into the Tomcat directory structure. (markt) Update: Update the packaged version of the Tomcat Native Library to 1.2.5 to pick up the Windows binaries that are based on OpenSSL 1.0.2g and APR 1.5.1. (markt) Update: Modify the default tomcat-users.xml file to make it harder for users to configure the entries intended for use with the examples web application for the Manager application. (markt) 2016-02-08 Tomcat 8.0.32 (markt)

General

Add: Allow to configure multiple JUnit test class patterns with the build property test.name and document the property in BUILDING.txt. (rjung) Fix: 58768: Log a warning if a redirect fails because of an invalid location. (markt) Catalina

Fix: Fix class loader decision on the delegation for class loading and resource lookup and make it faster too. (rjung) Fix: 58946: Ensure that the request parameter map remains immutable when processing via a RequestDispatcher. (markt) Fix: 58827: Deprecate what is left of the JSR 77 implementation. (markt) Fix: 58905: Ensure that Tomcat.silence() silences the correct logger and respects the current setting. (markt) Coyote

Add: New configuration option ajpFlush for the AJP connectors to disable the sending of AJP flush packets. (rjung) Cluster

Fix: Correct a regression in the session attribute filtering that prevented clustering from starting in the default configuration. (kfujino) WebSocket

Fix: Fix a timing issue on session close that could result in an exception being thrown for an incomplete message even through the message was completed. (markt) not released Tomcat 8.0.31 (markt)

Catalina

Fix: Correct implementation of validateClientProvidedNewSessionId so client provided session IDs may be rejected if validation is enabled. (markt) Fix: Add path parameter handling to HttpServletRequest.getContextPath(). This is a follow-up to the fix for 57215. (markt) Fix: 58692: Make StandardJarScanner more robust. Log a warning if a class path entry cannot be scanned rather than triggering the failure of the web application. Includes a test case written by Derek Abdine. (markt) Fix: 58701: Reset the instanceInitialized field in StandardWrapper when unloading a Servlet so that a new instance may be correctly initialized. (markt) Fix: 58702: Ensure an access log entry is generated if the client aborts the connection. (markt) Fix: Fixed various issues reported by Findbugs. (violetagg) Fix: 58735: Add support for the X-XSS-Protection header to the HttpHeaderSecurityFilter. Patch provided by Jacopo Cappellato. (markt) Fix: 58751: Correctly handle the case where an AsyncListener dispatches to a Servlet on an asynchronous timeout and the Servlet uses sendError() to trigger an error page. Includes a test case based on code provided by Andy Wilkinson.(markt) Fix: 58765: Change default for mapperContextRootRedirectEnabled to true since this is required for correct session management because of the default for sessionCookiePathUsesTrailingSlash. (markt) Fix: Add the StatusManagerServlet to the list of Servlets that can only be loaded by privileged applications. (markt) Fix: Simplify code and fix messages in org.apache.catalina.core.DefaultInstanceManager class. (kkolinko) Code: Deprecate InstanceListener, InstanceEvent and InstanceSupport prior to removal in 9.0.x. (markt) Fix: Ensure that the proper file encoding if specified will be used when a readme file is served by DefaultServlet. (violetagg) Fix: Fix declaration of localPort attribute of Connector MBean: it is read-only. (kkolinko) Fix: 58766: Make skipping non-class files during annotation scanning faster by checking the file name first. Improve debug logging. (kkolinko) Fix: 58809: Correctly recycle cookies when mapping requests for parallel deployment. As a side-effect of this fix, the system property org.apache.tomcat.util.http.ServerCookie.PRESERVE_COOKIE_HEADER is no longer used. From this release, Tomcat will always preserve the cookie header. (markt) Fix: 58836: Correctly merge query string parameters when processing a forwarded request where the target includes a query string that contains a parameter with no value. (markt/kkolinko) Fix: Make sure that shared Digester is reset in an unlikely error case in HostConfig.deployWAR(). (kkolinko) Fix: 58867: Improve checking on Host start for WAR files that have been modified while Tomcat has stopped and re-expand them if unpackWARs is true. (markt) Fix: Fix a potential JDBC resource leak in DataSourceRealm. (schultz) Fix: 58900: Correctly undeploy symlinked resources and prevent an infinite cycle of deploy / undeploy. (markt) Fix: Protect initialization of ResourceLinkFactory when running with a SecurityManager. (kkolinko) Add: Extend the feature available in the cluster session manager implementations that enables session attribute replication to be filtered based on attribute name to all session manager implementations. Note that configuration attribute name has changed from sessionAttributeFilter to sessionAttributeNameFilter. Apply the filter on load as well as unload to ensure that configuration changes made while the web application is stopped are applied to any persisted data. (markt) Add: Extend the session attribute filtering options to include filtering based on the implementation class of the value and optional WARN level logging if an attribute is filtered. These options are available for all of the Manager implementations that ship with Tomcat. When a SecurityManager is used filtering will be enabled by default. (markt) Jasper

Fix: Fix handling of missing messages in org.apache.el.util.MessageFactory. (violetagg) Cluster

Fix: In order to avoid that the heartbeat thread and the background thread to run Channel.heartbeat simultaneously, if heartbeatBackgroundEnabled of SimpleTcpCluster set to true, ensure that the heartbeat thread does not start. (kfujino) Code: Simplify the code of JvmRouteBinderValve.startInternal(). Avoid potential NPE when JvmRouteBinderValve is configured directly at Engine element. (kfujino) WebSocket

Fix: 57489: Ensure onClose() is called when a WebSocket connection is closed even if the sending of the close message fails. Includes test cases by Barry Coughlan. (markt) Web Applications

Add: Add a description of the default value of heartbeatSleeptime attribute and optionCheck attribute in the cluster channel docs. (kfujino) Fix: Correct some typos in the JNDI resources How-To. (markt) Fix: Don't create sessions unnecessarily in the Manager application. (markt) Fix: Don't create sessions unnecessarily in the Host Manager application. (markt) Fix: 58723: Clarify documentation and error messages for the text interface of the manager to make clear that version must be used with path when referencing contexts deployed using parallel deployment. (markt) Tribes

Fix: Fix potential NPE in AbstractReplicatedMap.breakdown(). (kfujino) Fix: Add support for the startup notification of local members in the static cluster. (kfujino) Fix: Ignore the unnecessary member remove operation from different domain. (kfujino) Fix: Add support for the shutdown notification of local members in the static cluster. (kfujino) Fix: Ensure that asynchronous session replication thread is a daemon thread. (kfujino) Other

Update: Remove native code (Windows Service Wrapper, APR/native connector) support for Windows Itanium. (markt) Update: Update the packaged version of the Tomcat Native Library to 1.2.4 to pick up the Windows binaries that are based on OpenSSL 1.0.2e and APR 1.5.1. (markt) Update: Update the NSIS Installer used to build the Windows Installers to version 2.50. (markt/kkolinko) Update: Update optional Checkstyle library to 6.14.1. (kkolinko) 2015-12-06 Tomcat 8.0.30 (markt)

Catalina

Fix: 34319: Only load those keys in StoreBase.processExpire from JDBCStore, that are old enough, to be expired. Based on a patch by Tom Anderson. (fschumacher) Add: 56917: As per RFC7231 (HTTP/1.1), allow HTTP/1.1 and later redirects to use relative URIs. This is controlled by a new attribute useRelativeRedirects on the Context and defaults to true. (markt) Fix: 58629: Allow an embedded Tomcat instance to start when the Service has no Engine configured. (markt) Fix: 58635: Enable break points to be set within agent code when running Tomcat with a Java agent. Based on a patch by Huxing Zhang. (markt) Fix: 58660: Correct a regression in 8.0.29 caused by the change that moved the redirection for context roots from the Mapper to the Default Servlet. (markt) Fix: Fixed potential NPE in HostConfig while deploying an application. Issue reported by coverity scan. (violetagg) Fix: 58655: Fix an IllegalStateException when calling HttpServletResponse.sendRedirect() with the RemoteIpFilter. This was caused by trying to correctly generate the absolute URI for the redirect. With the fix for 56917, redirects may now be relative making the sendRedirect() implementation for the RemoteIpFilter much simpler. This also addresses issues where the redirect may not have behaved as expected when redirecting from http to https to from https to http. (markt) Fix: 58657: Exceptions in a Servlet 3.1 ReadListener or WriteListener do not need to be immediately fatal to the connection. Allow an error response to be written. (markt) Coyote

Fix: Improve upgrade context classloader handling by using Context.bind and unbind. (remm) Jasper

Fix: 57136#c25: Change default value of quoteAttributeEL setting in Jasper to be true for better compatibility with other implementations and older versions of Tomcat (8.0.26/7.0.64 and earlier). Add command line option -no-quoteAttributeEL in JspC. (kkolinko) Cluster

Fix: Fix potential integer overflow in DeltaSession. Reported by coverity scan. (fschumacher) WebSocket

Add: 55006: The WebSocket client now honors the java.net.java.net.ProxySelector configuration (using the HTTP type) when establishing WebSocket connections to servers. Based on a patch by Niki Dokovski. (markt) Fix: 58624: Correct a thread safety issue that meant that blocking message writes could block indefinitely if the WebSocket connection was closed while a message write was in progress. (markt) Web Applications

Fix: 58631: Correct the continuation character use in the Windows Service How-To page of the documentation web application. (markt) Tribes

Fix: Ensure that the static member is registered to the add suspect list even if the static member that is registered to the remove suspect list has disappeared. (kfujino) Fix: Correct the warning log of when the member that is not registered in the membership is detected. (kfujino) Fix: When using a static cluster, add the members that have been cached in the membership service to the map members list in order to ensure that the map member is a static member. (kfujino) jdbc-pool

Fix: Correct evaluation of system property org.apache.tomcat.jdbc.pool.onlyAttemptCurrentClassLoader. It was basically ignored before. Reported by coverity scan. (fschumacher) Fix: Fix potential integer overflow in ConnectionPool and PooledConnection. Reported by coverity scan. (fschumacher) Other

Update: Update optional Checkstyle library to 6.13. (kkolinko) 2015-11-24 Tomcat 8.0.29 (markt)

General

Update: 58596: Clarify the description in RUNNING.txt of how environment variables are used. (markt) Catalina

Add: Extend the fix for 57136 to provide a JSP Servlet initialisation parameter per web application that controls whether or not EL in JSP attributes is processed as if it uses JSP attribute quoting. By default, EL does not use JSP attribute quoting. (markt) Fix: 57799: InputStream.available() was causing an IO operation to occur even in blocking mode, which caused problems with NIO2. (remm) Add: Extend the fix for 58228 to include ServletContext.getRealPath(). (markt) Add: 58486: Protect against two further possible memory leaks associated with XML parsing. (markt) Fix: 58490: Fixed NPE thrown when scanning for javax.servlet.ServletContainerInitializer in case the web application is not extracted. (violetagg) Code: 58497: Make AbstractHttp11Processor easy to extend. (markt) Fix: 58508: Escape role names when generating associated MBeans in case the role name contains characters not permitted in an MBean name. (markt) Fix: 58518: Correct a regression in the fix for 56777 that added support for URIs in config file locations. File paths on Windows could previously be specified with \ or / as the separator. 56777 broke that. (markt) Fix: 58519: Fix ISE thrown by web application classloader in some error conditions due to trying to call initCause() on a ClassNotFoundException which is not permitted. (markt) Fix: 58534: Removed repeated conditional tests in o.a.tomcat.websocket.pojo.PojoMethodMapping and o.a.tomcat.util.net.AprEndpoint Patch provided by Anthony Whitford. (violetagg) Fix: 58535: Use Collections.reverseOrder when a reverse ordering is needed. (violetagg) Fix: 58537, 58546: Some of the inner classes in o.a.catalina.valves.ExtendedAccessLogValve and o.a.tomcat.util.net.SecureNio2Channel are made static. Patch provided by Anthony Whitford. (violetagg) Fix: 58540: Removed unused code from o.a.catalina.connector.Request. Patch provided by Anthony Whitford. (violetagg) Fix: 58541, 58544: It is more efficient to call Integer.toString(int) instead of Integer.valueOf(int).toString() when only a string representation of a primitive is needed. Based on a patch provided by Anthony Whitford. (violetagg) Fix: 58541, 58547: It is more efficient to call valueOf(...) instead of Number constructor. Based on a patch provided by Anthony Whitford. (violetagg) Fix: 58545: In some use cases it is more efficient to use Map.entrySet() instead of Map.keySet() Based on a patch provided by Anthony Whitford. (violetagg) Fix: Ensure that ServletRequest.getContentLengthLong is used instead of ServletRequest.getContentLength for servlets and valves provided by Tomcat. The API is available since Servlet specification 3.1. (violetagg) Add: Add a new RestCsrfPreventionFilter that provides basic CSRF protection for REST APIs. (violetagg) Fix: 58578: Avoid NPE accessing cookies during access logging for request that had no context mapping. (remm) Fix: Avoid UnsupportedOperationException when releasing an user-provided URLStreamHandlerFactory. Patch provided by Cristian Talau. (violetagg) Fix: 58581: If a custom error page fails, fall back to the standard error page rather than throwing an NPE. Based on a patch by Huxing Zhang. (markt) Fix: 58582: Combined realm should perform background processing on its sub-realms. Based upon a patch provided by Aidan. (schultz) Fix: Handle the unlikely case where different versions of a web application are deployed with different session settings. (markt) Add: Add a new Context option, enabled by default, that enables an additional check that a client provided session ID is in use in at least one other web application before allowing it to be used as the ID for a new session in the current web application. (markt) Add: Add support for DIGEST authentication to the JNDIRealm. Based on a patch by Alexis Hassler. (markt) Fix: 58603: Ensure that HttpServletRequest.getRequestURL() returns the correct value when using the RemoteIpFilter. (markt) Fix: Ensure that in an embedded Tomcat the logging configuration is not lost during garbage collection. (violetagg) Add: Move the functionality that provides redirects for context roots and directories where a trailing / is added from the Mapper to the DefaultServlet. This enables such requests to be processed by any configured Valves and Filters before the redirect is made. This behaviour is configurable via the mapperContextRootRedirectEnabled and mapperDirectoryRedirectEnabled attributes of the Context which may be used to restore the previous behaviour. (markt) Coyote

Fix: Cancel pending blocking IO operation following a timeout in the NIO2 connector. (remm) Fix: Add instance manager support for upgrade handlers, and set context class loader. (remm) Update: Synchronize OpenSSL to JSSE cipher mapping to recent OpenSSL changes. In particular, TLSv1.0 is now an alias for those ciphers that require TLSv1 and will not work with SSLv3. TLSv1 remains an alias for SSLv3. (markt) Jasper

Add: Deprecate the STRICT_QUOTE_ESCAPING system property and replace it with an initialisation parameter for the JSP Servlet. This enables per web application control of this configuration setting. (markt) Cluster

Fix: Optimize the session lock range in DeltaManager.requestCompleted. (kfujino) Fix: Enable an explicit configuration of local member in the static cluster membership. (kfujino) Tribes

Code: Distinguish the handling of the shutdown payload and member verification clearly. When handling shutdown payload, verification completion message is not required. (kfujino) Fix: When starting the StaticMembershipInterceptor, StaticMembershipInterceptor checks the required Interceptors. If the required Interceptor does not exist, it issues warning logs. (kfujino) WebSocket

Fix: Use instance manager for server endpoint instances. (remm) Web applications

Add: Make it clear in the documentation for the CGI servlet that the debug page is not considered secure and should not be used in production. (markt) Fix: The domain attribute of StaticMember is not required but optional. (kfujino) jdbc-pool

Fix: 58489: Correct QueryStatsComparator to hold up the general contract for Comparator. (fschumacher) Fix: When creating a QueryStats object, ensure that maxQueries is checked. If maxQueries is a value less than or equal to 0, QueryStats are never created. (kfujino) Other

Update: Update optional Checkstyle library to 6.12.1. (kkolinko) Add: Add support for creating a FindBugs report when building Tomcat. It is disabled by default. (violetagg) 2015-10-12 Tomcat 8.0.28 (markt)

Catalina

Add: Add support for the custom classpath protocol in URLs. It an be used anywhere Tomcat accepts a URL for a configuration parameter. (markt) Fix: 56777: Allow file based configuration resources (user database, certificate revocation lists, keystores and trust stores) to be configured using URLs as well as files. (markt) Fix: Perform null-checking on input and stored credentials in all Realms before passing credentials off to CredentialHandlers for matching. (schultz) Coyote

Update: Add the new ciphers from RFC6655 and RFC7251 to the OpenSSL to JSSE cipher mapping. (markt) Update: Remove DES, RC2 and RC4 from DEFAULT for the OpenSSL to JSSE cipher mapping to align with the OpenSSL development branch. (markt) Jasper

Fix: Improve the error message when JSP parser encounters an error parsing an attribute value. (markt) Web applications

Update: 58474: Provide a reference to the differences between CATALINA_HOME and CATALINA_BASE in the sample application that is part of the documentation web application. (markt) Extras

Fix: Ensure JULI adapters does not include the LogFactoryImpl class. Patch provided by Benjamin Gandon. (markt) 2015-10-01 Tomcat 8.0.27 (markt)

Catalina

Fix: 58187: Correct a regression in the fix for 57765 that meant that deployment of web applications deployed via the Manager application was delayed until the next execution of the automatic deployment background process. (markt) Fix: 58284: Correctly implement session serialization so non-serializable attributes are skipped with a warning. Patch provided by Andrew Shore. (markt) Fix: 58313: Fix concurrent access of encoders map when clearing encoders prior to switch to async. (markt) Fix: 58320: Fix concurrent access of request attributes which is possible during asynchronous processing. (markt) Fix: 58352: Always trigger a thread dump if Tomcat fails to stop gracefully from catalina.sh even if using -force. Patch provided by Alexandre Garnier. (markt) Fix: 58368: Fix a rare data race in the code that obtains the ApplicationFilterFactory instance. (markt) Fix: 58369: Fix a rare data race in the code that obtains the CookieProcessor for a StandardContext instance. (markt) Fix: Ensure the JAASRealm uses the configured CredentialHandler. (markt) Fix: 58372: Fix rare data races closed and suspended flags that could be triggered by async and/or comet processing. (markt) Fix: 58373: Fix rare data race with the application event listeners for StandardContext. (markt) Fix: 58374: Fix a rare data race in the AsyncContext implementation for access to the internal Tomcat request object to which it holds a reference. (markt) Fix: 58380: Fix two rare data races in the standard session implementation on the flag that tracks if the session is new and on the field that tracks the maximum inactive period. (markt) Fix: 58385: Fix a rare data race in the internal flag Tomcat uses to keep track of whether or not a request is being used for Comet processing. (markt) Fix: 58394: Fix a rare data race in Mapper when adding or removing a host. (markt) Fix: 58398: Fix a rare data race in LifecycleSupport. (markt) Fix: 58412: Ensure that the AsyncFileHandler has the source class and method name available for logging. (fschumacher) Fix: 58416: Correctly detect when a forced stop fails to stop Tomcat because the Tomcat process is waiting on some system call or is uninterruptible. (markt) Fix: 58436: Fix some rare data races in JULI's ClassLoaderLogManager during shutdown. (markt) Fix: 58845: Fix off-by one error in calculation of valid characters in a cookie domain. Patch provided by Thorsten Ehlers. (markt) Coyote

Fix: Correct some edge cases in RequestUtil.normalize(). (markt) Fix: 58275: The IBM JREs accept cipher suite names starting with TLS_ or SSL_ but when listing the supported cipher suites only the SSL_ version is reported. This can break Tomcat's check that at least one requested cipher suite is supported. Tomcat now includes a work-around so either form of the cipher suite name can be used when running on an IBM JRE. (markt) Fix: 58357: For reasons not currently understood when the APR/native connector is used with OpenSSL reads can return an error code when there is no apparent error. This was work-around for HTTP upgrade connections by treating this as EAGAIN. The same fix has now been applied to the standard HTTP connector. (markt) Code: Minor clean-up in NIO2 SSL handshake code to address some theoretical concurrency issues. (markt) Fix: 58367: Fix a rare data race in the code that obtains the reason phrase for a given HTTP response code. (markt) Fix: 58370: Fix a rare data race in the connector shutdown code. (markt) Fix: 58371: Fix a rare data race when accessing request URI in String form when switching from non-async to async due to early triggering of the gathering of request statistics. (markt) Fix: 58375: Fix a rare data race on the internal flag Tomcat uses to mark a response as committed. (markt) Fix: 58377: Fix a rare data race on the internal flag Tomcat uses to mark a request as using HTTP keep-alive when switching to asynchronous processing. (markt) Fix: 58379: Fix a rare data race on the internal reference Tomcat retains to the socket when switching to asynchronous processing. (markt) Fix: 58387: Fix a rare data race when closing Comet connections. (markt) Fix: 58388: Fix a data race when determining if Comet processing is occurring on a container or non-container thread. (markt) Fix: 58389: Fix a rare data race while shutting down the thread pools on Connector stop. (markt) Code: Clean up use of error flag on socket wrapper prompted by 58390. (markt) Code: Remove some unnecessary code from the NIO Poller and fix 58396 as a side-effect. (markt) Fix: 57799: Remove useless sendfile check for NIO SSL. (remm) Jasper

Fix: 57136: Correct a regression in the previous fix for this issue. \${ should only be an escape for ${ within an EL expression. Within a JSP page \$ should be an escape for $. The EL specification applies when parsing the expression delimited by ${ and }. Parsing of the delimiting ${ and } is the responsibility of the JSP specification. (markt) Fix: 58296: Fix a memory leak in the JSP unloading feature that meant that using a value other than -1 for maxLoadedJsps triggered a memory leak once the limit was reached. (markt) Fix: 58327: Cache the expression string for value expression literals since it is frequently used and may be expensive to evaluate. Patch provided by Andreas Kohn. (markt) Fix: 58340: Improve error reporting for tag files packaged in JARs. (markt) Fix: 58424: When parsing TLD files, allow whitespace around boolean configuration values. (schultz) Fix: Fix a possible resource leak reported by coverity scan. (fschumacher) Fix: 58427: Enforce the JSP specification defined limitations of which elements are allowed in an implicit.tld file. (markt) Fix: 58444: Ensure that JSPs work with any custom base class that meets the requirements defined in the JSP specification without requiring that base class to implement Tomcat specific code. (markt) Cluster

Fix: Fix a default clusterListeners in SimpleTcpCluster. The optimal default value is different for each session manager. ClusterSessionListener is never used in BackupManager. (kfujino) Fix: Correct log messages in case of using BackupManager. (kfujino) WebSocket

Fix: 58342: Fix a copy and paste error that meant MessageHandler removal could fail for binary and pong MessageHandlers. Patch provided by DJ. (markt) Fix: Data races detected by RV-Predict, mostly caused by completion handlers running in separate threads. (markt) Fix: 58414: Correctly handle sending zero length messages when using per message deflate. (markt) Web applications

Fix: Correct documentation for cluster-howto. (kfujino) Fix: Add missing documentation for property alwaysAddExpires for the LegacyCookieProcessor. (markt) Tribes

Add: Add support for configurations of ChannelListener and MembershipListener in server.xml. (kfujino) Fix: Correct log messages in case of using ReplicatedMap. (kfujino) Fix: 58381: Fix a rare data race in the NioReceiver. (markt) Fix: 58382: Fix multiple rare data races in the default membership implementation. (markt) Fix: 58383: Fix a data race in SenderState. (markt) Fix: 58386: Fix a data race in ObjectReader. (markt) Fix: 58391: Fix multiple data races in NonBlockingCoordinator, most of which were associated with ensuring that log messages contained the correct information. (markt) Fix: 58392: Fix a data race in DomainFilterInterceptor. (markt) Fix: 58393: Fix a data race on the listener in McastService. (markt) Fix: 58395: Fix multiple data races in MemberImpl that were likely to cause issues if certain properties were updated concurrently (such updates are unlikely in normal usage). (markt) Code: Remove some unnecessary code from PooledParallelSender and fix 58397. (markt) jdbc-pool

Fix: Make sure the pool has been properly configured when attributes that related to the pool size are changed via JMX. (kfujino) Other

Fix: Ensure logging works for all tests in a class rather than just the first one executed. (markt) Add: 58344: Add build properties to enable tests to be executed against alternative binaries. Based on a patch by Petr Sumbera. (markt) 2015-08-21 Tomcat 8.0.26 (markt)

Web applications

Add: 58255: Document the Semaphore valve. Patch provided by Kyohei Nakamura. (markt) not released Tomcat 8.0.25 (markt)

Catalina

Fix: Make the WAR manifest file available for WebResource instances from an unpacked WAR in the same way the manifest is available if the WAR is not unpacked. (markt) Fix: Ensure that only /WEB-INF/classes/ and /WEB-INF/lib/ are excluded from the web resource caching. (Resources loaded from these locations are cached by the web application class loader.) (markt) Add: 57741: Enable the CGI servlet to use the standard error page mechanism. Note that if the CGI servlet's debug init parameter is set to 10 or higher then the standard error page mechanism will be bypassed and a debug response generated by the CGI servlet will be returned instead. (markt) Fix: 58031: Make the (first) reason parameter parsing failed available as a request attribute and then use it to provide a better status code via the FailedRequstFilter (if configured). (markt) Fix: 58086: Correct a regression in the fix for 58086 that incorrectly handled WAR URLs. (violetagg) Fix: 58096: Classes loaded from /WEB-INF/classes/ should use that directory as their code base. (markt) Fix: Fix possible resource leaks by closing streams properly. Issues reported by Coverity Scan. (violetagg) Fix: 58116: Fix regression in the fix for 57281 that broke Comet support when running under a security manager. Based on a patch provided by Johno Crawford. (markt) Fix: 58125: Avoid a possible ClassCircularityError when running under a security manager. (markt) Fix: 58179: Fix a thread safety issues that could mean concurrent threads setting the same attribute on a ServletContext could both see null as the old value. (markt) Fix: Allow web archives bigger than 2G to be deployed using ANT tasks. (violetagg) Fix: 58192: Correct a regression in the previous fix for 58023. Ensure that classes are associated with their manifest even if the class file is first read (and cached) without the manifest. (markt) Fix: Fix thread safety issue in the AsyncContext implementation that meant a sequence of start();dispatch(); calls using non-container threads could result in a previous dispatch interfering with a subsequent start. (markt) Fix: 58228: Make behaviour of ServletContext.getResource() and ServletContext.getResourceAsStream() consistent with each other and the expected behaviour of the GET_RESOURCE_REQUIRE_SLASH system property. (markt) Fix: 58230: Fix input stream corruption if non-blocking I/O is used and the first read is made immediately after the switch to async mode rather than in response to onDataAvaiable() and that read does not read all the available data. (markt) Fix: Ensure that log4javascript*.jar was not excluded from the standard JAR scanning by default. (markt) Coyote

Fix: 57943: Prevent the same socket being added to the cache twice. Patch based on analysis by Ian Luo / Sun Qi. (markt) Fix: Add text/javascript,application/javascript to the default list of compressable MIME types. (violetagg) Fix: 58103: When pipelining requests, and the previous request was an async request, ensure that the socket is removed from the waiting requests so that the async timeout thread doesn't process it during the next request. (markt) Fix: 58151: Correctly handle EOF in the AJP APR/native connector to prevent the connector entering a loop and generate excessive CPU load. (markt) Fix: In the AJP and HTTP NIO connectors, ensure that the socket timeout is correctly set before adding the socket back to the poller for read. (markt) Fix: 58157: Ensure that the handling of async timeouts does not result in an unnecessary dispatch to a container thread that could result in the current socket being added to the Poller multiple times with multiple attempts to process the same event for the same socket. (markt) Fix: Correct a couple of edge cases in RequestUtil.normalize(). (markt) Jasper

Fix: 58110: Like scriptlet sections, declaration sections of JSP pages have a one-to-one mapping of lines to the generated .java file. Use this information to provide more accurate error messages if a compilation error occurs in a declaration section. (markt) Fix: 58119: When tags are compiled they must be placed in the org/apache/jsp/tag/web directory. Correct a regression in the fix for 52725. (violetagg) Fix: Fix a resource leak in JspC identified by Eclipse. (markt) Fix: 58178: Expressions in a tag file should use the tag file's PageContext rather than that of the containing page. (markt) Fix: Following on from the fix for 58178, expressions in a tag file should use the tag file's imports rather than those of the containing page. (markt) WebSocket

Fix: 58166: Allow applications to send close codes in the range 3000-4999 inclusive. (markt) Fix: 58232: Avoid possible NPE when adding endpoints programmatically to the javax.websocket.server.ServerContainer. Based on a patch provided by bastian.(violetagg) Web applications

Fix: Correct the incorrect document of QueryTimeoutInterceptor. The setting value is not in milliseconds but in seconds. (kfujino) Fix: 58112: Update the documentation for using the Catalina tasks in an Apache Ant build file. (markt) Fix: Improve the Javadoc for some of the APR socket read functions that have inconsistent behaviour for return values. (markt) jdbc-pool

Fix: 58042: The default value of logFailed attribute of SlowQueryReport is changed to false so that the failed queries are not logged by default. (kfujino) Fix: Fix potential NPE in QueryTimeoutInterceptor. (kfujino) Fix: Add support for stopping the pool cleaner via JMX. (kfujino) Fix: The fairness attribute and ignoreExceptionOnPreLoad attribute do not allow a change via JMX. (kfujino) Fix: If the timeBetweenEvictionRunsMillis attribute is changed via jmx, it should restart the pool cleaner because this attribute affects the execution interval of the pool cleaner. (kfujino) Fix: Eliminate the dependence on maxActive of busy queues and idle queue in order to enable the expansion of the pool size via JMX. (kfujino) Other

Update: Update optional Checkstyle library to 6.8.1. (kkolinko) Fix: Update sample Eclipse IDE configuration to exclude test/webapp* and similar paths from compiler sourcepath. (kkolinko) Update: Update package renamed Apache Commons Pool to Commons Pool 2.4.2. (markt) Update: Update package renamed Apache Commons DBCP to Commons DBCP 2.1.1. (markt) Add: Support the use of the threads attribute on Ant's junit task. Note that using this with a value of greater than one will disable Cobertura code coverage. (markt) 2015-07-06 Tomcat 8.0.24 (markt)

Catalina

Fix: 57938: Correctly handle empty form fields when a form is submitted as multipart/form-data, the maxPostSize attribute of the Connector has been set to a negative value and the Context has been configured with a value of true for allowCasualMultipartParsing. The meaning of the value zero for the maxPostSize has also been changed to mean a limit of zero rather than no limit to align it with maxSavePostSize and to be more intuitive. (markt) Fix: 57977: Correctly bind and unbind the web application class loader during execution of the PersistentValve. (markt) Fix: Remove some unnecessary code from the web application class loader and deprecate the now unused validate() method since the requirements of SRV.10.7.2 are met using cleaner code in loadClass(String, boolean) and filter(). (markt) Fix: Correct a bug that prevented the web application class loader's filter() from working correctly. It only returned true for classes in sub-packages of the listed packages, but not classes located in the packages themselves. (markt) Fix: Add the WebSocket API classes to the list of classes that the web application class loader will always delegate to its parent for loading first. (markt) Fix: 58015: Ensure that whenever the web application class loader checks to see if it should delegate first, it also checks the result of the filter() method which may indicate that it should always delegate first for the current class/resource regardless of the value of the delegate configuration option. (markt) Fix: 58023: Fix potentially excessive memory usage due to unnecessary caching of JAR manifests in the web application class loader. (markt) Fix: 57700: Ensure that Container event ADD_CHILD_EVENT will be sent in all cases. (violetagg) Fix: 58086: Ensure that WAR URLs are handled properly when using ANT for web application deployment. Based on a patch provided by Lukasz Jader. (violetagg) Fix: Fix CredentialHandler element handling in storeconfig. (remm) Coyote

Fix: 57265: Further fix to address a potential threading issue when sendfile is used in conjunction with TLS. (markt) Fix: 57936: Improve robustness of the acceptor thread count parameter for NIO2, since it must be set to 1. Submitted by Oliver Kant. (remm) Add: 57943: Added a work-around to catch ConcurrentModificationExceptions during Poller timeout processing that were causing the Poller thread to stop. The root cause of these exceptions is currently unknown. (markt) Fix: 57944: Ensure that if non-blocking I/O listeners are set on a non-container thread that the expected listener events are still triggered. (markt) Fix: Fix possible very long (1000 seconds) timeout with APR/native connector. (markt) Add: Support "-" separator in the SSLProtocol configuration of the APR/native connector for protocol exclusion. (rjung) Fix: 58004: Fix AJP buffering output data even in blocking mode. (remm) WebSocket

Fix: 57969: Provide path parameters to POJO via per session javax.websocket.server.ServerEndpointConfig as they vary between different requests. (violetagg) Fix: 57974: Session.getOpenSessions should return all sessions associated with a given endpoint instance, rather than all sessions from the endpoint class. (remm) Web applications

Fix: 57282: Update request processing sequence diagrams. Updated diagrams provided by Stephen Chen. (markt) Fix: 57971: Correct the documentation for the cluster configuration setting recoverySleepTime. (markt) Add: 57758: Add document of testOnConnect attribute in jdbc-pool doc. (kfujino) Add: Add description of validatorClassName attribute to testXXXX attributes in jdbc-pool docs. (kfujino) Tribes

Code: Use StringManager to provide i18n support in the org.apache.catalina.tribes packages. (kfujino) Fix: Do not set the nodes that failed to replication to the backup nodes. Ensure that the nodes that the data has been successfully replicated are set to the backup node. (kfujino) Fix: When failed to replication, rather than all member is handled as a failed member, exclude the failure members from backup members. (kfujino) jdbc-pool

Fix: Refactoring of the removeOldest method in SlowQueryReport to behave as expected. (kfujino) Fix: 57783: Fix NullPointerException in SlowQueryReport. To avoid this NPE, Refactor SlowQueryReport#removeOldest and handle the abandoned connection properly. (kfujino) Fix: 58042: In SlowQueryReportJmx, the LogSlow and logFailed attributes that inherited from SlowQueryReport are used as a condition of whether JMX notifications are sent. (kfujino) Fix: Ensure that specified Boolean attribute values of SlowQueryReport reflect correctly. The LogSlow and the logFailed are not system property, these are attributes of SlowQueryReport. (kfujino) Other

Update: Update package renamed Apache Commons BCEL to r1682271 to pick up some some code clean up. (markt) Update: Update package renamed Apache Commons DBCP to r1682314 to pick up the DBCP 2.1 release and additional fixes since then. (markt) Update: Update package renamed Apache Commons Pool to the 2.4 release. (markt) Update: Update package renamed Apache Commons File upload to r1682322 to pick up the post 1.3.1 fixes. (markt) Update: Update package renamed Apache Commons Codec to r1682326. No functional changes. Javadoc only. (markt) Update: Update optional Checkstyle library to 6.7. (kkolinko) 2015-05-22 Tomcat 8.0.23 (markt)

Catalina

Add: 54618: Add a new HttpHeaderSecurityFilter that adds the Strict-Transport-Security, X-Frame-Options and X-Content-Type-Options HTTP headers to the response. (markt) Fix: 57875: Add javax.websocket.* to the classes for which the web application class loader always delegates first. (markt) Fix: 57871: Ensure that setting the allowHttpSepsInV0 property of a LegacyCookieProcessor to false only prevents HTTP separators from being used without quotes. (markt) Fix: Add a workaround for issues with SPNEGO authentication when running on Java 8 update 40 and later. The workaround should be safe for earlier Java versions but it can be disabled with the applyJava8u40Fix attribute of the SPNEGO authenticator if necessary. (markt) Fix: 57926: Restore the original X-Forwarded-By and X-Forwarded-For headers after processing by the RemoteIPValve . (markt) Coyote

Fix: Follow up to previous fix that removed the behavior difference between NIO and NIO2 for SSL, which caused corruption with NIO2. (remm) Fix: 57931: Ensure that TLS connections with the NIO or NIO2 HTTP connectors that experience issues during the handshake (e.g. missing or invalid client certificate) are closed cleanly and that the client receives the correct error code rather than simply closing the connection. (markt) Jasper

Fix: 56438: Add debug logging to TLD discovery that logs positive and negative results for JARs, resource paths and directories. Patch provided by VIN. (markt) Fix: 57802: Correct the default implementation of convertToType() provided by javax.el.ELResolver. (markt) Fix: 57887: Fix compilation of recursive tag files packaged in a JAR. (markt) Cluster

Fix: Make sure that stream is closed after using it in DeltaSession.applyDiff(). (kfujino) Code: Use StringManager to provide i18n support in the org.apache.catalina.ha packages. (kfujino) Code: Add the context name to log messages when replication context failed to start. (kfujino) Web applications

Fix: 57875: Update the web application class loader documentation to reflect the more relaxed approach to SRV.10.7.2 in Tomcat 8 onwards. (markt) Fix: 57896: Document system property org.apache.tomcat.util.http.ServerCookie.PRESERVE_COOKIE_HEADER that was introduced in Tomcat 8.0.0. (kkolinko) Tribes

Fix: Ensure that the state transfer flag is updated to true only when the map states have been transferred correctly from existing map members. (kfujino) Other

Update: Update optional Checkstyle library to 6.6. (kkolinko) 2015-05-05 Tomcat 8.0.22 (markt)

Catalina

Fix: 57736: Change the format of the Tomcat specific URLs for resources inside JARs that are in turn packed in a WAR. The ^/ sequence has been replaced by */ so that the resulting URLs are compliant with RFC 2396 and do not trigger exceptions when converted to URIs. The old format will continue to be accepted. (markt) Fix: 57752: Exclude non-cached resources from the Cache statistics for resource lookups. Patch provided by Adam Mlodzinski. (markt) Add: Allow logging of the remote port in the access log using the format pattern %{remote}p. (rjung) Fix: 57556: Refine the previous fix for this issue so that the real path returned only has a trailing separator if the requested path ended with /. (markt) Fix: 57765: When checking last modified times as part of the automatic deployment process, account for the fact that File.lastModified() has a resolution of one second to ensure that if a file has been modified within the last second, the latest version of the file is always used. Note that a side-effect of this change is that files with modification times in the future are treated as if they are unmodified. (markt) Fix: Align redeploy resource modification checking with reload modification checking so that now, in both cases, a change in modification time rather than an increase in modification time is used to determine if the resource has changed. (markt) Fix: Cleanup o.a.tomcat.util.digester.Digester from debug messages that do not give any valuable information. Patch provided by Polina Genova. (violetagg) Fix: 57772: When reloading a web application and a directory representing an expanded WAR needs to be deleted, delete the directory after the web application has been stopped rather than before to avoid potential ClassNotFoundExceptions. (markt) Fix: Fix wrong logger name of org.apache.catalina.webresources.StandardRoot. (kfujino) Fix: 57801: Improve the error message in the start script in case the PID read from the PID file is already owned by a process. (rjung) Fix: 57841: Improve error logging during web application start. (markt) Fix: 57856: Ensure that any scheme/port changes implemented by the RemoteIpFilter also affect HttpServletResponse.sendRedirect(). (markt) Fix: 57863: Fix the RewriteMap support in RewriteValve that did not use the correct key value to look up entries. Based on a patch provided by Tatsuya Bessho. (markt) Coyote

Fix: 57779: When an I/O error occurs on a non-container thread only dispatch to a container thread to handle the error if using Servlet 3+ asynchronous processing. This avoids potential deadlocks if an application is performing I/O on a non-container thread without using the Servlet 3+ asynchronous API. (markt) Code: Remove the experimental support for SPDY. No current user agent supports the version of SPDY that the experiment targeted. Note: HTTP/2 support is under development for Tomcat 9 and may be back-ported to Tomcat 8 once complete. (markt) Fix: Possible incomplete writes with SSL NIO2. (remm) Fix: Incorrect reads with SSL NIO2 caused by a bad strategy for handling IO differences between NIO and NIO2 that don't seem to be justified. (remm) Fix: After some errors, the pending flags could remain set when using SSL NIO2. (remm) Fix: 57833: When using JKS based keystores for NIO or NIO2, ensure that the key alias is always converted to lower case since that is what JKS key stores expect. Based on a patch by Santosh Giri Govind M. (markt) Fix: 57837: Add text/css to the default list of compressable MIME types. (markt) Jasper

Fix: 57845: Ensure that, if the same JSP is accessed directly and via a declaration in web.xml, updates to the JSP are visible (subject to the normal rules on re-compilation) regardless of how the JSP is accessed. (markt) Fix: 57855: Explicitly handle the case where a MethodExpression is invoked with null or the wrong number of parameters. Rather than failing with an ArrayIndexOutOfBoundsException or a NullPointerException throw an IllegalArgumentException with a useful error message. (markt) Cluster

Fix: Avoid unnecessary call of DeltaRequest.addSessionListener() in non-primary nodes. (kfujino) Add: Add new attribute that send all actions for session across Tomcat cluster nodes. (kfujino) Fix: Remove unused pathname attribute in mbean definition of BackupManager. (kfujino) WebSocket

Fix: 57761: Ensure that the opening HTTP request is correctly formatted when the WebSocket client connects to a server root. (remm) Fix: 57762: Ensure that the WebSocket client correctly detects when the connection to the server is dropped. (markt) Fix: 57776: Revert the 8.0.21 fix for the permessage-deflate implementation and incorrect op-codes since the fix was unnecessary (the bug only affected trunk) and the fix broke rather than fixed permessage-deflate if an uncompressed message was converted into more than one compressed message. (markt) Fix: Fix log name typo in WsRemoteEndpointImplServer class, caused by a copy-paste. (markt/kkolinko) Fix: 57788: Avoid NPE when looking up a class hierarchy without finding anything. (remm) Web applications

Add: 57759: Add information to the keyAlias documentation to make it clear that the order keys are read from the keystore is implementation dependent. (markt) Fix: 57864: Update the documentation web application to make it clearer that hex values are not valid for cluster send options. Based on a patch by Kyohei Nakamura. (markt) Tribes

Fix: Fix a concurrency issue when a backup message that has all session data and a backup message that has diff data are processing at the same time. This fix ensures that MapOwner is set to ReplicatedMapEntry. (kfujino) Other

Fix: Add missing pom for tomcat-storeconfig. (remm) Update: Update optional Checkstyle library to 6.5. (kkolinko) Fix: 57707: Improve error message when trying to run a release build on a non-Windows platform and Wine is not available. (markt) 2015-03-26 Tomcat 8.0.21 (markt)

Catalina

Add: 49785: Enable StartTLS connections for JNDIRealm. (fschumacher) Fix: When docBase refers internal war and unpackWARs is set to false, avoid registration of the invalid redeploy resource that has been added ".war" extension in duplicate. (kfujino) Fix: If WAR exists, it is not necessary to trigger a reload when adding a Directory. (kfujino) Fix: 55988: Add support for Java 8 JSSE server-preferred TLS cipher suite ordering. This feature requires Java 8 and is controlled by useServerCipherSuitesOrder attribute on an HTTP connector. Based upon a patch provided by Ognjen Blagojevic. (schultz) Fix: 56608: When deploying an external WAR, add watched resources in the expanded directory based on whether the expanded directory is expected to exist rather than if it does exist. (markt) Fix: When triggering a reload due to a modified watched resource, ensure that multiple changed watched resources only trigger one reload rather than a series of reloads. (markt) Fix: 57601: Ensure that HEAD requests return the correct content length (i.e. the same as for a GET) when the requested resource includes a resource served by the Default servlet. (jboynes/markt) Fix: 57602: Ensure that HEAD requests return the correct content length (i.e. the same as for a GET) when the requested resource includes a resource served by a servlet that extends HttpServlet. (markt) Fix: 57621: When an async request completes, ensure that any remaining request body data is swallowed. (markt) Fix: 57637: Do not create unnecessary sessions when using PersistentValve. (jboynes/fschumacher) Fix: 57645: Correct a regression in the fix for 57190 that incorrectly required the path passed to ServletContext.getContext(String) to be an exact match to a path to an existing context. (markt) Fix: Make sure that unpackWAR attribute of Context is handled correctly in HostConfig. (kfujino) Fix: When deploying a WAR file that contains a context.xml file and unpackWARs is false ignore any context.xml file that may exist in an expanded directory associated with the WAR. (markt) Fix: 57675: Correctly quote strings when using the extended access log. (markt) Add: Enable Tomcat to detect when a WAR file has been changed while Tomcat is not running. Tomcat does this by adding a META-INF/war-tracking file to the expanded directory and setting the last modified time of this file to the last modified time of the WAR. If Tomcat detects a modified WAR via this mechanism the web application will be redeployed (i.e. the expanded directory will be removed and the modified WAR expanded in its place). (markt) Fix: 57704: Fix potential NPEs during web application start/stop when org.apache.tomcat.InstanceManager is not initialized. (violetagg) Add: Use the simplified digest output for digest.bat|sh when generating digests with no salt and a single iteration to make it easier to use with DIGEST authentication. (markt) Fix: Add support for LAST_ACCESS_AT_START system property to SingleSignOn. (kfujino) Code: Refactor Authenticator implementations to reduce code duplication. (markt) Fix: 57724: Handle the case in the CORS filter where a user agent includes an origin header for a non-CORS request. (markt) Fix: When searching for SCIs o.a.catalina.Context.getParentClassLoader will be used instead of java.lang.ClassLoader.getParent. Thus one can provide the correct parent class loader when running embedded Tomcat in other environments such as OSGi. (violetagg) Fix: 57743: Fix a locked file / resource leak issue when a JAR is accessed just before or during web application undeploy. Patch provided by Pavel Avgustinov. (markt) Coyote

Add: 57540: Make TLS/SSL protocol available in a new request attribute (org.apache.tomcat.util.net.secure_protocol_version). (Note that AJP connectors will require mod_jk 1.2.41 or later, or an as-yet-unknown version of mod_proxy_ajp, or configure the proxy to send the AJP_SSL_PROTOCOL request attribute to Tomcat. Please see the bug comments for details.) Based upon a patch provided by Ralf Hauser. (schultz) Fix: Fix a cipher ordering issue when using the OpenSSL syntax for JSSE cipher configuration to ensure that ephemeral ECDH with AES is preferred to ephemeral ECDH with anything else. (markt) Fix: 57570: Make the processing of trailer headers with chunked input optional and disabled by default. (markt) Fix: 57592: Correctly handle the case where an AsyncContext is used for non-blocking I/O and is completed during a write operation. (markt) Fix: 57638: Avoid an IllegalArgumentException when an AJP request body chunk larger than the socket read buffer is being read. This typically requires a larger than default AJP packetSize. (markt) Fix: 57674: Avoid a BufferOverflowException when an AJP response body chunk larger than the socket write buffer is being written. This typically requires a larger than default AJP packetSize. (markt) Update: Align the OpenSSL syntax cipher configuration with the OpenSSL 1.0.2 branch. (markt) Fix: Numerous fixes to the APR/native connector to improve robustness. (markt) Fix: Stop caching and re-using SocketWrapper instances. With the introduction of upgrade and non-blocking I/O, I/O can occur on non-container threads. This makes it nearly impossible to track whether a SocketWrapper is still being referenced or not, making re-use a risky proposition. (markt) Code: Refactor Connector authentication (only used by AJP) into a separate method. (markt) Add: 57708: Implement a new feature for AJP connectors - Tomcat Authorization. If the new tomcatAuthorization attribute is set to true (it is disabled by default) Tomcat will take an authenticated user name from the AJP protocol and use the appropriate Realm for the request to authorize (i.e. add roles) to that user. (markt) Fix: Fix an issue that meant that any pipe-lined data read by Tomcat before an asynchronous request completed was lost during the completion of the asynchronous request. This mean that the pipe-lined request(s) would be lost and/or corrupted. (markt) Update: Update the minimum recommended version of the Tomcat Native library (if used) to 1.1.33. (markt) Jasper

Fix: 57135: Package imports via javax.el.ImportHandler should only import public, concrete classes. (markt) Fix: 57583: Cache 'Not Found' results in javax.el.ImportHandler.resolveClass() to save repeated attempts to load classes that are known not to exist to improve performance. (markt) Fix: 57626: Correct a regression introduced in the 8.0.16 fix for ensuring Jars were closed after use, that broke recompilation of modified JSPs that depended on a tag file packaged in a Jar. (markt) Fix: 57627: Correctly determine last modified times for dependencies when a tag file packaged in a JAR depends on a tag file packaged in a second JAR. (markt) Fix: 57647: Ensure INFO message is logged when scanning jars for TLDs if the scan does not find a TLD in any jar. Previously a message would only be logged if a TLD was not found in all scanned jars. (jboynes) Update: 57662: Update all references to the ECJ compiler to version 4.4.2. (violetagg) Cluster

Fix: Remove unnecessary method that always returns true. The domain filtering works on DomainFilterInterceptor. (kfujino) WebSocket

Fix: Correct a bug in the permessage-deflate implementation that meant that the incorrect op-codes were used if an uncompressed message was converted into more than one compressed message. (markt) Add: 57676: List conflicting WebSocket endpoint classes when there is a path conflict. Based upon a patch proposed by yangkun. (schultz) Web applications

Fix: 56058: Add links to the AccessLogValve documentation for configuring reverse proxies and/or Tomcat to ensure that the desired information is used entered in the access log when Tomcat is running behind a reverse proxy. (markt) Fix: 57587: Update the JNDI Datasource HOWTO for DBCP2. Patch provided by Phil Steitz. (markt) Fix: Remove incorrect note from context configuration page in the documentation web application that stated WAR files located outside the appBase were never unpacked. (markt) Update: 57644: Update examples to use Apache Standard Taglib 1.2.5. (jboynes) Fix: 57683: Ensure that if a client aborts their connection to the stock ticker example (the only way a client can disconnect), the example continues to work for existing and new clients. (markt) Fix: Make it clear that when using digested passwords with DIGEST authentication that no salt and only a single iteration must be used when generating the digest. (markt) Extras

Fix: 57377: Remove the restriction that prevented the use of SSL when specifying a bind address with the JMXRemoteLifecycleListener. Also enable SSL to be configured for the registry as well as the server. (markt) Tribes

Fix: When a map member has been added to ReplicatedMap, make sure to add it to backup nodes list of all other members. (kfujino) Fix: Make sure that refuse the messages from a different domain in DomainFilterInterceptor. (kfujino) Other

Update: Update optional Checkstyle library to 6.4.1. (kkolinko) Fix: 57703: Update the http-method definition for web applications using a Servlet 2.5 descriptor as per Servlet 2.5 MR 6. (markt) Update: Update to Tomcat Native Library version 1.1.33 to pick up the Windows binaries that are based on OpenSSL 1.0.1m and APR 1.5.1. (markt) 2015-02-20 Tomcat 8.0.20 (markt)

Coyote

Fix: Fix a concurrency issue that meant that a change in socket timeout (e.g. when switching to asynchronous I/O) did not always take effect immediately. (markt) not released Tomcat 8.0.19 (markt)

Catalina

Fix: Clarify threaded usage of variables by removing volatile marker in NonceInfo. Issue reported by Coverity Scan. (fschumacher) Fix: 57180: Further fixes to support the use of arbitrary HTTP methods with the CORS filter. (markt) Fix: 57472: Fix performance regression in resources implementation when signed JARs are used in a web application. (markt) Add: Warn about problematic setting of appBase. (fschumacher) Fix: Fix exception while authentication in JDBCRealm. (fschumacher) Fix: 57534: CORS Filter should only look at media type component of Content-Type request header. (markt) Fix: 57556: Align getRealPath() behaviour with that of earlier versions and include a trailing separator if the real path refers to a directory. (markt) Fix: Ensure that Servlet 3.0 async requests where startAsync() is called in one container thread and dispatch() is called in a different container thread complete correctly. (markt) Fix: Ensure that user name checking in the optional SecurityListener is case-insensitive (as documented) and than the case-insensitive comparison is performed using the system default Locale. (markt) Add: 57021: Improve logging in AprLifecycleListener and jni.Library when Tomcat-Native DLL fails to load. Based on a patch by Pravallika Peddi. (markt/kkolinko) Coyote

Fix: Fix several bugs that could cause multiple registrations for write events for a single socket when using Servlet 3.0 async. Typically, the side effects of these multiple registrations would be exceptions appearing in the logs. (markt) Fix: 57432: Align SSL_OP_NO_TLSv1_1 and SSL_OP_NO_TLSv1_2 constant values with OpenSSL (they had been swapped). (markt) Fix: 57509: Improve length check when writing HTTP/1.1 response headers: reserve space for 4 extra bytes. (kkolinko) Fix: 57544: Fix potential infinite loop when preparing a kept alive HTTP connection for the next request. (markt) Fix: 57546: Ensure that a dropped network connection does not leave references to the UpgradeProcessor associated with the connection in memory. (markt) Fix: When applying the maxSwallowSize limit to a connection read that many bytes first before closing the connection to give the client a chance to read the response. (markt) Fix: Prevent an async timeout being processed multiple times for the same socket when running on slow and/or heavily loaded systems. (markt) Fix: 57581: Change statistics byte counter in coyote Request object to be long to allow values above 2Gb. (kkolinko) Update: Use the data that supports cipher definition using OpenSSL syntax to improve the quality of values provided for the javax.servlet.request.key_size request attribute. (markt) Fix: Fix a concurrency issue in the APR Poller that meant it was possible under low load for a socket queued to be added to the Poller not to be added for 10 seconds. (markt) Jasper

Update: 57123: Update all references to the ECJ compiler to version 4.4.1. With thanks to Ralph Schaer for uploading the 4.4.1 JAR to Maven Central. (markt) Add: 57564: Make JspC amenable to subclassing. Patch provided by Jan Bartel. (markt) Fix: Simplify code in ProtectedFunctionMapper class of Jasper runtime. (kkolinko) Fix: 57574: Do not check existence of a Java package in javax.el.ImportHandler.importPackage(). (kkolinko) WebSocket

Fix: 57490: Make it possible to use Tomcat's WebSocket client within a web application when running under a SecurityManager. Based on a patch by Mikael Sterner. (markt) Add: Add some debug logging to the WebSocket session to track session creation and session closure. (markt) Web applications

Update: Clarify documentation for useBodyEncodingForURI attribute of a connector. (kkolinko) Fix: Fix possible resource leaks by closing streams properly. Issues reported by Coverity Scan. (fschumacher) Fix: 57503: Make clear that the JULI integration for log4j only works with log4j 1.2.x. (markt) Fix: 57496: Remove hard-coded URL in JSP SVG example. (markt) Tribes

Fix: Fix a possible deadlock when receiver thread invokes mapMemberAdded() while ping thread invokes memberAlive(). (kfujino) Other

Add: Enhance bean factory used for JNDI resources. New attribute forceString allows to support non-standard string argument property setters. (rjung) Fix: Assign newly created stream to field instead of leaking it uselessly. Issue reported by Coverity Scan. (fschumacher) Update: Update optional Checkstyle library to 6.3. (kkolinko) Fix: Guard the digester from MbeansDescriptorsDigesterSource with its own lock object. (fschumacher) Fix: Refactor the unit tests and add some new test properties to make it easier to exclude performance tests and relax timing tests. This is primarily for the ASF CI system where these tests frequently fail. (markt) Fix: 57558: Add missing JAR in Ant task definition required by the validate task. (markt) Add: List names of Testsuites that have failed or skipped tests when running the tests with Ant. (kkolinko) 2015-01-26 Tomcat 8.0.18 (markt)

Catalina

Fix: 57178: The CORS filter now treats null as a valid origin that matches *. Patch provided by Gregor Zurowski. (markt) Fix: 57425: Don't add attributes with null value or name to the replicated context. (fschumacher) Add: 57431: Enable usage of custom class for context creation when using embedded tomcat. (fschumacher) Fix: 57446: Ensure that ServletContextListeners that have limited access to ServletContext methods are called with the same ServletContext instance for both contextInitialized() and contextDestroyed(). (markt) Fix: 57455: Explicitly block the use of the double-quote character when configuring the common, server and shared class loaders since double-quote is used to quote values that contain commas. (markt) Fix: 57461: When an instance of org.apache.catalina.startup.VersionLoggerListener logs the result of System.getProperty("java.home") don't report it in a manner that makes it look like the JAVA_HOME environment variable. (markt) Fix: 57476: Ensure the responses written as part of a forward are fully written. This fixes a regression in 8.0.15 caused by the fix for 57252. (markt) Fix: While closing streams for given resources ensure that if an exception happens it will be handled properly. Issue is reported by Coverity Scan. (violetagg) Fix: 57481: Fix IllegalStateException at the end of the request when using non-blocking reads with the HTTP BIO connector. (markt) Fix: Change Response to use UEncoder instances with shared safeChars. (fschumacher) Fix: Ensure that when static resources are served from JARs, only static resources are served. (markt) Add: Allow VersionLoggerListener to log all system properties. This feature is off by default. (kkolinko) Jasper

Fix: Ensure that classes imported via the page directive are made available to the EL environment via the ImportHandler. Issue is reported by Coverity Scan. (violetagg) Fix: 57441: Do not trigger an error when using functions defined by lambdas or imported via an ImportHandler in an EL expression in a JSP. (markt) Cluster

Fix: Fix mbean descriptor of ClusterSingleSignOn. (kfujino) Fix: 57473: Add sanity check to FarmWebDeployer's WarWatcher to detect suspected incorrect permissions on the watch directory. (schultz) Tribes

Fix: Clarify the handling of Copy message and Copy nodes. (kfujino) Fix: Copy node does not need to send the entry data. It is enough to send only the node information of the entry. (kfujino) Fix: ReplicatedMap should send the Copy message when replicating. (kfujino) Fix: Fix behavior of ReplicatedMap when member has disappeared. If map entry is primary, rebuild the backup members. If primary node of map entry has disappeared, backup node is promoted to primary. (kfujino) 2015-01-16 Tomcat 8.0.17 (markt)

Catalina

Fix: Correct a regression in the previous fix for 57252 that broke request listeners for non-async requests that triggered an error that was handled by the ErrorReportingValve. (markt/violetagg) Coyote

Fix: Add flushing to send ack in the NIO2 connector. (remm) not released Tomcat 8.0.16 (markt)

Catalina

Fix: 57172: Provide a better error message if something attempts to access a resource through a web application class loader that has been stopped. (markt/kkolinko) Fix: 57173: Revert the fix for 56953 that broke annotation scanning in some cases. (markt) Fix: 57180: Do not limit the CORS filter to only accepting requests that use an HTTP method defined in RFC 7231. (markt) Fix: 57190: Fix ServletContext.getContext(String) when parallel deployment is used so that the correct ServletContext is returned. (markt) Fix: 57208: Prevent NPE in JNDI Realm when no results are found in a directory context for a user with specified user name. Based on a patch provided by Jason McIntosh. (violetagg) Add: 57209: Add a new attribute, userSearchAsUser to the JNDI Realm. (markt) Fix: 57215: Ensure that the result of calling HttpServletRequest.getContextPath() is neither decoded nor normalized as required by the Servlet specification. (markt) Fix: 57216: Improve handling of invalid context paths. A context path should either be an empty string or start with a '/' and do not end with a '/'. Invalid context path are automatically corrected and a warning is logged. The null and "/" values are now correctly changed to "". (markt/kkolinko) Fix: Update storeconfig with the CredentialHandler element. (remm) Fix: Correct message that is logged when load-on-startup servlet fails to load. It was logging a wrong name. (kkolinko) Fix: 57239: Correct several message typos. Includes patch by vladk. (kkolinko) Fix: Fix closing of Jars during annotation scanning. (schultz/kkolinko) Fix: Fix a concurrency issue in async processing. Ensure that a non-container thread can not change the async state until the container thread has completed. (markt) Fix: 57252: Provide application configured error pages with a chance to handle an async error before the built-in error reporting. (markt) Fix: 57281: Enable non-public Filter and Servlet classes to be configured programmatically via the Servlet 3.0 API and then used without error when running under a SecurityManager. (markt) Fix: 57308: Remove unnecessary calls to System.getProperty() where more suitable API calls are available. (markt) Add: Add unit tests for RemoteAddrValve and RemoteHostValve. (rjung) Add: Allow to configure RemoteAddrValve and RemoteHostValve to adopt behavior depending on the connector port. Implemented by optionally adding the connector port to the string compared with the patterns allow and deny. Configured using addConnectorPort attribute on valve. (rjung) Add: Optionally trigger authentication instead of denial in RemoteAddrValve and RemoteHostValve. This only works in combination with preemptiveAuthentication on the application context. Configured using invalidAuthenticationWhenDeny attribute on valve. (rjung) Fix: Remove the obsolete jndi protocol usage from the scanning process performed by StandardJarScanner. (violetagg) Fix: Prevent file descriptors leak and ensure that files are closed after retrieving the last modification time. (violetagg) Update: Make o.a.catalina.webresources.StandardRoot easier for extending. (violetagg) Fix: 57326: Enable AsyncListener implementations to re-register themselves during AsyncListener.onStartAsync. (markt) Fix: 57331: Allow ExpiresFilter to use "year" as synonym for "years" in its configuration. (kkolinko) Fix: Ensure that if the RewriteValve rewrites a request that subsequent calls to HttpServletRequest.getRequestURI() return the undecoded URI. (markt) Fix: Ensure that if the RewriteValve rewrites a request to a non-normalized URI that the URI is normalized before the URI is mapped to ensure that the correct mapping is applied. (markt) Fix: Prevent NPEs being logged during post-processing for requests that have been re-written by the RewriteValve. (markt) Fix: Various StoreConfig improvements including removing a dependency on the StandardServer implementation, improve consistency of behaviour when MBean is not registered and improve error messages when accessed via the Manager application. (markt) Update: Improve SnoopServlet in unit tests. (rjung) Add: Add RequestDescriptor class to unit tests. Adjust TestRewriteValve to use RequestDescriptor. (rjung) Update: Add more AJP unit tests. (rjung) Fix: 57363: Log to stderr if LogManager is unable to read configuration files rather than swallowing the exception silently. (markt) Coyote

Fix: Allow HTTP upgrade process to complete without data corruption when additional content is sent along with the upgrade header. (remm) Fix: 57187: Regression handling the special * URL. (remm) Fix: 57234: Make SSL protocol filtering to remove insecure protocols case insensitive. (markt) Fix: 57265: Fix some potential concurrency issues with sendFile and the NIO connector. (markt) Fix: 57324: If the client uses Expect: 100-continue and Tomcat responds with a non-2xx response code, Tomcat also closes the connection. If Tomcat knows the connection is going to be closed when committing the response, Tomcat will now also send the Connection: close response header. (markt) Fix: 57340: When using Comet, ensure that Socket and SocketWrapper are only returned to their respective caches once on socket close (it is possible for multiple threads to call close concurrently). (markt) Fix: 57347: AJP response contains wrong status reason phrase (rjung) Add: 57391: Allow TLS Session Tickets to be disabled when using the APR/native HTTP connector. Patch provided by Josiah Purtlebaugh. (markt) Jasper

Fix: 57142: As per the clarification from the JSP specification maintenance lead, classes and packages imported via the page directive must be made available to the EL environment via the ImportHandler. (markt) Fix: 57247: Correct the default Java source and target versions in the JspC usage message to 1.7 for Java 7. (markt) Fix: 57309: Ensure that the current EL Resolver is given an opportunity to perform type coercion before applying the default EL coercion rules. (markt) Fix: Improve the calculation of the resource's last-modified, performed by JspCompilationContext, in a way to support URLs with protocol different than jar:file. (violetagg) Fix: CVE-2014-7810: Do not use a privileged code block when evaluating EL expressions when running under a security manager, which allowed to bypass code restrictions. (markt) Fix: Fix an issue with BeanELResolver when running under a security manager. Some classes may not be accessible but may have accessible interfaces. (markt) Cluster

Fix: In order to enable define in Cluster element, ClusterSingleSignOn implements ClusterValve. (kfujino) Fix: 57338: Improve the ability of the ClusterSingleSignOn valve to handle nodes being added and removed from the Cluster at run time. (markt) WebSocket

Fix: Correct multiple issues with the flushing of batched messages that could lead to duplicate and/or corrupt messages. (markt) Fix: Correctly implement headers case insensitivity. (markt/remm) Fix: Allow optional use of user extensions. (remm) Fix: Allow using partial binary message handlers. (remm) Fix: Limit ping/pong message size. (remm) Fix: Allow configuration of the time interval for the periodic event. (remm) Fix: More accurate annotations processing. (remm) Fix: Allow optional default for origin header in the client. (remm) Web applications

Fix: Update documentation for CGI servlet. Recommend to copy the servlet declaration into web application instead of enabling it globally. Correct documentation for cgiPathPrefix. (kkolinko) Update: Improve HTML version of build instructions and align with BUILDING.txt. (kkolinko) Update: Improve Tomcat Manager documentation. Rearrange, add section on HTML GUI, document /expire command and Server Status page. (kkolinko) Update: 57238: Update information on SSL/TLS on Security and SSL documentation pages. Patch by Glen Peterson. (kkolinko) Fix: 57245: Correct the reference to allowLinking in the security configuration guide since that attribute has moved from the Context element to the nested Resources element. (markt) Fix: Fix ambiguity of section links on Valves configuration reference page. (kkolinko) Fix: 57261: Fix vminfo and threaddump Manager commands to start their output with an "OK" line. Document them. Based on a patch by Oleg Trokhov. (kkolinko) Fix: 57267: Document the StoreConfigLifecycleListener and the /save command for the Manager application. (markt) Fix: 57323: Correct display of outdated sessions in sessions count listing in Manager application. (kkolinko) Add: Add document of ClusterSingleSignOn. (kfujino) Other

Update: When downloading required libraries at build time, use random name for temporary file and automatically create destination directory (base.path). (kkolinko) Update: Update optional Checkstyle library to 6.2. (kkolinko) Update: Simplify setproxy task in build.xml. Taskdef there is not needed since Ant 1.8.2. (kkolinko) Fix: Update "ide-eclipse" target in build.xml to create Eclipse project that uses Java 7 compliance settings instead of workspace-wide defaults. (kkolinko) Fix: Update the package renamed copy of Apache Commons Pool 2 to the 2.3 release to pick up various fixes since the 2.2 release including one for a possible infinite loop. (markt) Fix: 57285: Restore the manifest entry that marks the Windows uninstaller application as requiring elevated privileges. (markt) Add: 57344: Provide sha1 checksum files for Tomcat downloads. Correct filename patterns for apache-tomcat-*-embed.tar.gz archive to exclude an *.asc file. (kkolinko) 2014-11-07 Tomcat 8.0.15 (markt)

Catalina

Add: 43548: Add an XML schema for the tomcat-users.xml file. (markt) Add: 43682: Add support for referring to the current context, host and service name in per Context logging.properties files by using the properties ${classloader.webappName}, ${classloader.hostName} and ${classloader.serviceName}. (markt) Add: 47919: Extend the information logged when Tomcat starts to optionally log the values of command line arguments (enabled by default) and environment variables (disabled by default). Note that the values added to CATALINA_OPTS and JAVA_OPTS environment variables will be logged, as they are used to build up the command line. (markt) Add: 49939: Expose the method that clears the static resource cache for a web application via JMX. (markt) Fix: 55951: Allow cookies to use UTF-8 encoded values in HTTP headers. This requires the use of the RFC6265 CookieProcessor. (markt) Fix: 55984: Using the allow separators in version 0 cookies option with the legacy cookie processor should only apply to version 0 cookies. Version 1 cookies with values that contain separators should not be affected and should continue to be quoted. (markt) Add: 56393: Add support for RFC6265 cookie parsing and generation. This is currently disabled by default and may be enabled via the CookieProcessor element of a Context. (markt) Add: 56394: Introduce new configuration element CookieProcessor in Context to allow context-specific configuration of cookie processing options. Attributes of Context element that were added in Tomcat 8.0.13 to allow configuration of a new experimental RFC6265 based cookie parser (useRfc6265 and cookieEncoding) are replaced by this new configuration element. (markt) Fix: Improve the previous fix for 56401. Avoid logging version information in the constructor since it then gets logged at undesirable times such as when using StoreConfig. (markt) Fix: 56403: Add pluggable password derivation support to the Realms via the new CredentialHandler interface. (markt/schultz) Fix: 57016: When using the PersistentValve do not remove sessions from the store when persisting them. (markt) Add: Deprecate the use of system properties to control cookie parsing and replace them with attributes on the new CookieProcessor that may be configured on a per context basis. (markt) Fix: Correct an edge case and allow a cookie if the value starts with an equals character and the CookieProcessor is not configured to allow equals characters in cookie values but is configured to allow name only cookies. (markt) Fix: 57022: Ensure SPNEGO authentication continues to work with the JNDI Realm using delegated credentials with recent Oracle JREs. (markt) Fix: 57027: Add additional validation for stored credentials used by Realms when the credential is stored using hex encoding. (markt) Fix: 57038: Add a WebResource.getCodeBase() method, implement for all WebResource implementations and then use it in the web application class loader to set the correct code base for resources loaded from JARs and WARs. (markt) Fix: Correct a couple of NPEs in the JNDI Realm that could be triggered with when not specifying a roleBase and enabling roleSearchAsUser. (markt) Fix: Correctly handle relative values for the docBase attribute of a Context. (markt) Fix: Ensure that log messages generated by the web application class loader correctly identify the associated Context when multiple versions of a Context with the same path are present. (markt) Fix: Remove the unnecessary registration of context.xml as a redeploy resource. The context.xml having an external docBase has already been registered as a redeploy resource at first. (kfujino) Fix: 57089: Ensure that configuration of a session ID generator is not lost when a web application is reloaded. (markt) Fix: 57105: When parsing web.xml do not limit the buffer element of the jsp-property-group element to integer values as the allowed values are kb or none. (markt) Update: Update the minimum required version of the Tomcat Native library (if used) to 1.1.32. (markt) Fix: Update storeconfig with newly introduced elements: SessionIdGenerator, CookieProcessor, JarScanner and JarScanFilter. (remm) Fix: Throw a NullPointerException if a null string is passed to the write(String,int,int) method of the PrintWriter obtained from the ServletResponse. (markt) Fix: Cookie rewrite flag abbreviation should be CO rather than C. (remm) Fix: 57153: When the StandardJarScanner is configured to scan the full class path, ensure that class path entries added directly to the web application class loader are scanned. (markt) Fix: AsyncContext should remain usable until fireOnComplete is called. (remm) Fix: AsyncContext createListener should wrap any instantiation exception using a ServletException. (remm) Fix: 57155: Allow a web application to be configured that does not have a docBase on the file system. This is primarily intended for use when embedding. (markt) Fix: Propagate header ordering from fileupload to the part implementation. (remm) Coyote

Add: 53952: Add support for TLSv1.1 and TLSv1.2 for APR connector. Based upon a patch by Marcel Šebek. This feature requires Tomcat Native library 1.1.32 or later. (schultz/jfclere) Code: Cache the Encoder instances used to convert Strings to byte arrays in the Connectors (e.g. when writing HTTP headers) to improve throughput. (markt) Add: Disable SSLv3 by default for JSSE based HTTPS connectors (BIO, NIO and NIO2). The change also ensures that SSLv2 is disabled for these connectors although SSLv2 should already be disabled by default by the JRE. (markt) Add: Disable SSLv3 by default for the APR/native HTTPS connector. (markt) Fix: Do not increase remaining counter at end of stream in IdentityInputFilter. (kkolinko) Fix: Trigger an error if an invalid attempt is made to use non-blocking IO. (markt) Fix: 57157: Allow calls to AsyncContext.start(Runnable) during non-blocking IO reads and writes. (markt) Fix: Async state MUST_COMPLETE should still be started. (remm) Jasper

Fix: 57099: Ensure that semi-colons are not permitted in JSP import page directives. (markt) Fix: 57113: Fix broken package imports in Expression Language when more than one package was imported and the desired class was not in the last package imported. (markt) Fix: 57132: Fix import conflicts reporting in Expression Language. (kkolinko) Fix: When coercing an object to a given type, only attempt coercion to an array if both the object type and the target type are an array type. (violetagg/markt) Fix: Improve handling of invalid input to javax.el.ImportHandler.resolveClass(). (markt) Fix: Allow the same class to be added to an instance of javax.el.ImportHandler more than once without triggering an error. The second and subsequent calls for the same class will be ignored. (markt) Fix: 57136: Ensure only \${ and #{ are treated as escapes for ${ and #{ rather than \$ and # being treated as escapes for $ and # when processing literal expressions in expression language. (markt) Fix: When coercing an object to an array type in Expression Language, handle the case where the source object is an array of primitives. (markt/kkolinko) Fix: Do not throw an exception on missing JSP file servlet initialization. (remm) Fix: 57148: When coercing an object to a given type and a PropertyEditor has been registered for the type correctly coerce the empty string to null if the PropertyEditor throws an exception. (kkolinko/markt) Fix: 57153: Correctly scan for TLDs located in directories that represent expanded JARs files that have been added to the web application class loader's class path. (markt) Fix: 57141: Enable EL in JSPs to refer to static fields of imported classes including the standard java.lang.* imports. (markt) Cluster

Fix: Add support for the SessionIdGenerator to cluster manager template. (kfujino) Fix: Avoid possible integer overflows reported by Coverity Scan. (fschumacher) WebSocket

Fix: 57054: Correctly handle the case in the WebSocket client when the HTTP response to the upgrade request can not be read in a single pass; either because the buffer is too small or the server sent the response in multiple packets. (markt) Add: Extend support for the permessage-deflate extension to the client implementation. (markt) Fix: Fix client subprotocol handling. (remm) Fix: Add null checks for arguments in remote endpoint. (remm/kkolinko) Fix: 57091: Work around the behaviour of the Oracle JRE when creating new threads in an applet environment that breaks the WebSocket client implementation. Patch provided by Niklas Hallqvist. (markt) Fix: 57118: Ensure that that an EncodeException is thrown by RemoteEndpoint.Basic.sendObject(Object) rather than an IOException when no suitable Encoder is configured for the given Object. (markt) Web applications

Fix: Correct a couple of broken links in the Javadoc. (markt) Fix: Correct documentation for ServerCookie.ALLOW_NAME_ONLY system property. (kkolinko) Fix: 57049: Clarified that jvmRoute can be set in 's jvmRoute or in a system property. (schultz) Fix: Correct version of Java WebSocket mentioned in documentation (s/1.0/1.1/). (markt/kkolinko) Update: Suppress timestamp comments in Javadoc. (kkolinko) Fix: 57147: Various corrections to the JDBC Store section of the session manager configuration page of the documentation web application. (markt) Tribes

Fix: 45282: Improve shutdown of NIO receiver so that sockets are closed cleanly. (fhanik/markt) jdbc-pool

Fix: 57005: Fix javadoc errors when building with Java 8. Patch provided by Pierre Viret. (markt) Fix: 57079: Use Tomcat version number for jdbc-pool module when building and shipping the module as part of Tomcat. (markt) Fix: Fix broken overview page in javadoc generated via "javadoc" task in jdbc-pool build.xml file. (kkolinko) Other

Fix: 56079: The uninstaller packaged with the Apache Tomcat Windows installer is now digitally signed. (markt) Fix: Fix timestamps in Tomcat build and jdbc-pool to use 24-hour format instead of 12-hour one and use UTC timezone. (markt/kkolinko) Fix: Update the package renamed copy of Apache Commons DBCP 2 to revision 1631450 to pick up additional fixes since the 2.0.1 release including Javadoc corrections to fix errors when compiling with Java 8. (markt) Update: 56596: Update to Tomcat Native Library version 1.1.32 to pick up the Windows binaries that are based on OpenSSL 1.0.1j and APR 1.5.1. (markt) Code: In Tomcat tests: log name of the current test method at start time. (kkolinko) 2014-09-29 Tomcat 8.0.14 (markt)

Other

Fix: 56079: The Apache Tomcat Windows installer, the Apache Tomcat Windows service and the Apache Tomcat Windows service monitor application are now digitally signed. (markt) not released Tomcat 8.0.13 (markt)

Catalina

Fix: 55917: Allow bytes in the range 0x80 to 0xFF to appear in cookie values if the cookie is a V1 (RFC2109) cookie and the value is correctly quoted. The new RFC6265 based cookie parser must be enabled to correctly handle these cookies. (markt) Fix: 55918: Do not permit control characters to appear in quoted V1 (RFC2109) cookie values. The new RFC6265 based cookie parser must be enabled to correctly handle these cookies. (markt) Fix: 55921: Correctly handle (ignore the cookie) unescaped JSON in a cookie value. The new RFC6265 based cookie parser must be enabled to correctly handle these cookies. (markt) Add: 56401: Log version information when Tomcat starts. (markt/kkolinko) Add: 56530: Add a web application class loader implementation that supports the parallel loading of web application classes. (markt) Fix: 56900: Fix some potential resource leaks when reading property files reported by Coverity Scan. Based on patches provided by Felix Schumacher. (markt) Fix: 56902: Fix a potential resource leak in the Default Servlet reported by Coverity Scan. Based on a patch provided by Felix Schumacher. (markt) Fix: 56903: Correct the return value for StandardContext.getResourceOnlyServlets() so that multiple names are separated by commas. Identified by Coverity Scan and fixed based on a patch by Felix Schumacher. (markt) Add: Add an additional implementation of a RFC6265 based cookie parser along with new Context options to select and configure it. This parser is currently considered experimental and is not used by default. (markt) Fix: Fixed the multipart elements merge operation performed during web application deployment. Identified by Coverity Scan. (violetagg) Fix: Correct the information written by ExtendedAccessLogValve when a format token x-O(XXX) is used so that multiple values for a header XXX are separated by commas. Identified by Coverity Scan. (violetagg) Fix: Fix a potential resource leak when reading MANIFEST.MF file for extension dependencies reported by Coverity Scan. (violetagg) Fix: Fix some potential resource leaks when reading properties, files and other resources. Reported by Coverity Scan. (violetagg) Fix: Correct the previous fix for 56825 that enabled pre-emptive authentication to work with the SSL authenticator. (markt) Code: Refactor to reduce code duplication identified by Simian. (markt) Fix: When using parallel deployment and undeployOldVersions feature is enabled on a Host, correctly undeploy context of old version. Make sure that Tomcat does not undeploy older Context if current context is not running. (kfujino) Fix: Fix a rare threading issue when locking resources via WebDAV. (markt) Fix: Fix a rare threading issue when using HTTP digest authentication. (markt) Fix: When deploying war, add XML file in the config base to the redeploy resources if war does not have META-INF/context.xml or deployXML is false. If XML file is created in the config base, redeploy will occur. (kfujino) Code: Various changes to reduce unnecessary code in Tomcat's copy of Apache Commons BCEL to reduce the time taken for annotation scanning when web applications start. Includes contributions from kkolinko and hzhang9. (markt) Fix: 56938: Ensure web applications that have mixed case context paths and are deployed as directories are correctly removed on undeploy when running on a case sensitive file system. (markt) Add: 57004: Add stuckThreadCount property to StuckThreadDetectionValve's JMX bean. Patch provided by Jiří Pejchal. (schultz) Fix: 57011: Ensure that the request and response are correctly recycled when processing errors during async processing. (markt) Coyote

Fix: 56910: Prevent the invalid value of -1 being used for maxConnections with APR connectors. (markt) Fix: Ensure that AJP connectors enable the KeepAliveTimeout. (kfujino) Fix: Reduce duplicated code. All AJP connectors use common method to configuration of processor. (kfujino) Jasper

Fix: 43001: Enable the JspC Ant task to set the JspC option mappedFile. (markt) Fix: Ensure that the implementation of javax.servlet.jsp.PageContext.include(String) and javax.servlet.jsp.PageContext.include(String, boolean) will throw IOException when an I/O error occur during the operation. (violetagg) Fix: 56908: Fix some potential resource leaks when reading jar files. Reported by Coverity Scan. Patch provided by Felix Schumacher. (violetagg) Fix: Fix a potential resource leak in JDTCompiler when checking whether a resource is a package. Reported by Coverity Scan. (fschumacher) Fix: 56991: Deprecate the use of a request attribute to pass a declaration to Jasper and prevent an infinite loop if this technique is used in conjunction with an include. (markt) WebSocket

Fix: 56905: Make destruction on web application stop of thread group used for WebSocket connections more robust. (kkolinko/markt) Fix: 56907: Ensure that client IO threads are stopped if a secure WebSocket client connection fails. (markt) Fix: 56982: Return the actual negotiated extensions rather than an empty list for Session.getNegotiatedExtensions(). (markt) Update: Update the WebSocket implementation to support the Java WebSocket specification version 1.1. (markt) Web applications

Add: Add JarScanner to the nested components listed for a Context. (markt) Update: Update the Windows authentication documentation after some additional testing to answer the remaining questions. (markt) Other

Fix: 56895: Correctly compose JAVA_OPTS in catalina.bat so that escape sequences are preserved. Patch by Lucas Theisen. (markt) Update: 56988: Allow to use relative path in base.path setting when building Tomcat. (kkolinko) Fix: 56990: Ensure that the ide-eclipse build target downloads all the libraries required by the default Eclipse configuration files. (markt) Fix: Update the package renamed copy of Apache Commons DBCP 2 to revision 1626988 to pick up the fixes since the 2.0.1 release including support for custom eviction policies. (markt) Fix: Update the package renamed copy of Apache Commons Pool 2 to revision 1627271 to pick up the fixes since the 2.2 release including some memory leak fixes and support for application provided eviction policies. (markt) 2014-09-03 Tomcat 8.0.12 (markt)

Catalina

Add: Make the session id generator extensible by adding a SessionIdGenerator interface, an abstract base class and a standard implementation. (rjung) Fix: 56882: Fix regression in processing of includes and forwards when Context have been reloaded. Tomcat was responding with HTTP Status 503 (Servlet xxx is currently unavailable). (kkolinko) Coyote

Fix: When building a list of JSSE ciphers from an OpenSSL cipher definition, ignore unknown criteria rather than throwing a NullPointerException. (markt) Add: Add support for the EECDH alias when using the OpenSSL cipher syntax to define JSSE ciphers. (markt) Jasper

Fix: Correct a logic error in the JasperElResolver. There was no functional impact but the code was less efficient as a result of the error. Based on a patch by martinschaef. (markt) Fix: 56568: Enable any HTTP method to be used to request a JSP page that has the isErrorPage page directive set to true. (markt) WebSocket

Add: Extend support for the permessage-deflate extension to compression of outgoing messages on the server side. (markt) Other

Add: 56323: Include the *.bat files when installing Tomcat via the Windows installer. (markt) 2014-08-22 Tomcat 8.0.11 (markt)

Catalina

Fix: 56658: Fix regression that a context was inaccessible after reload. (kkolinko) Fix: 56710: Do not map requests to servlets when context is being reloaded. (kkolinko) Fix: 56712: Fix session idle time calculations in PersistenceManager. (kkolinko) Fix: 56717: Fix duplicate registration of MapperListener during repeated starts of embedded Tomcat. (kkolinko) Add: 56724: Write an error message to Tomcat logs if container background thread is aborted unexpectedly. (kkolinko) Fix: When scanning class files (e.g. for annotations) and reading the number of parameters in a MethodParameters structure only read a single byte (rather than two bytes) as per the JVM specification. Patch provided by Francesco Komauli. (markt) Fix: Allow the JNDI Realm to start even if the directory is not available. The directory not being available is not fatal once the Realm is started and it need not be fatal when the Realm starts. Based on a patch by Cédric Couralet. (markt) Fix: 56736: Avoid an incorrect IllegalStateException if the async timeout fires after a non-container thread has called AsyncContext.dispatch() but before a container thread starts processing the dispatch. (markt) Fix: 56739: If an application handles an error on an application thread during asynchronous processing by calling HttpServletResponse.sendError(), then ensure that the application is given an opportunity to report that error via an appropriate application defined error page if one is configured. (markt) Fix: 56784: Fix a couple of rare but theoretically possible atomicity bugs. (markt) Fix: 56785: Avoid NullPointerException if directory exists on the class path that is not readable by the Tomcat user. (markt) Fix: 56796: Remove unnecessary sleep when stopping a web application. (markt) Fix: 56801: Improve performance of org.apache.tomcat.util.file.Matcher which is to filter JARs for scanning during web application start. Based on a patch by Sheldon Shao. (markt) Fix: 56815: When the gzip option is enabled for the DefaultServlet ensure that a suitable Vary header is returned for resources that might be returned directly in compressed form. (markt) Fix: Do not mark threads from the container thread pool as container threads when being used to process AsyncContext.start(Runnable) so processing is correctly transferred back to a genuine container thread when necessary. (markt) Add: Add simple caching for calls to StandardRoot.getResources() in the new (for 8.0.x) resources implementation. (markt) Fix: 56825: Enable pre-emptive authentication to work with the SSL authenticator. Based on a patch by jlmonteiro. (markt) Fix: 56840: Avoid NPE when the rewrite valve is mapped to a context. (remm) Fix: Correctly handle multiple accept-language headers rather than just using the first header to determine the user's preferred Locale. (markt) Fix: 56848: Improve handling of accept-language headers. (markt) Fix: 56857: Fix thread safety issue when calling ServletContext methods while running under a security manager. (markt) Coyote

Fix: Fix NIO2 sendfile state tracking and error handling to fix various corruption issues. (remm) Fix: Missing timeout for NIO2 sendfile writes. (remm) Fix: Allow inline processing for NIO2 sendfile and optimize keepalive behavior. (remm) Fix: Fix excessive NIO2 sendfile direct memory use in some cases, sendfile will now instead use the regular socket write buffer as configured. (remm) Fix: 56661: Fix getLocalAddr() for AJP connectors. The complete fix is only available with a recent AJP forwarder like the forthcoming mod_jk 1.2.41. (rjung) Fix: Use default ciphers defined as HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5 so that no weak ciphers are enabled by default. (remm) Fix: 56780: Enable Tomcat to start when using SSL with an IBM JRE in strict SP800-131a mode. (markt) Fix: 56810: Remove use of Java 8 specific API calls in unit tests for OpenSSL to JSSE cipher conversion. (markt) Jasper

Fix: 56709: Fix system property name in a log message. Submitted by Robert Kish. (remm) Fix: 56797: When matching a method in an EL expression, do not treat bridge methods as duplicates of the method they bridge to. In this case always call the target of the bridge method. (markt) WebSocket

Fix: 56746: Allow secure WebSocket client threads to use the current context class loader rather than explicitly setting it to the class loader that loaded the WebSocket implementation. This allows WebSocket client connections from within web applications to access, amongst other things, the JNDI resources associated with the web application. (markt) Web applications

Fix: Correct the label in the list of sessions by idle time for the bin that represents the idle time immediately below the maximum permitted idle time when using the expire command of the Manager application. (markt) jdbc-pool

Fix: 53088: More identifiable thread name. (fhanik) Fix: 53200: Selective logging for slow versus failed queries. (fhanik) Fix: 53853: More flexible classloading. (fhanik) Fix: 54225: Disallow empty init SQL. (fhanik) Fix: 54227: Evaluate max age upon borrow. (fhanik) Fix: 54235: Disallow nested pools exploitating using data source. (fhanik) Fix: 54395: Fix JDBC interceptor parsing bug. (fhanik) Fix: 54537: Performance improvement in StatementFinalizer. (fhanik) Fix: 54978: Make sure proper connection validation always happens, regardless of config. (fhanik) Fix: 56318: Ability to trace statement creation in StatementFinalizer. (fhanik) Fix: 56789: getPool() returns the actual pool, always. (fhanik) Other

Add: 56788: Display the full version in the list of installed applications when installed via the Windows installer package. Patch provided by Alexandre Garnier. (markt) Add: 56829: Add the ability for users to define their own values for _RUNJAVA and _RUNJDB environment variables. Be more strict with executable filename on Windows (s/java/java.exe/). Based on a patch by Neeme Praks. (markt/kkolinko) not released Tomcat 8.0.10 (markt)

Catalina

Fix: 44312: Log an error if there is a conflict between Host and Alias names. Improve host management methods in Mapper to avoid occasionally removing a wrong host. Check that host management operations are performed on the host and not on an alias. (kkolinko) Code: 56611: Refactor code to remove inefficient calls to Method.isAnnotationPresent(). Based on a patch by Jian Mou. (markt/kkolinko) Fix: Fix regression in StandardContext.removeApplicationListener(), introduced by the fix for bug 56588. (kkolinko) Fix: 56653: Fix concurrency issue with lists of contexts in Mapper when stopping Contexts. (kkolinko) Fix: 56657: When using parallel deployment, if the same session id matches different versions of a web application, prefer the latest version. Ensure that remapping selects the version that we expect. (kkolinko) Fix: Assert that mapping result object is empty before performing mapping work in Mapper. (kkolinko) Code: Remove context and wrapper fields in Request class and deprecate their setters. (kkolinko) Fix: 56658: Avoid delay between registrations of mappings for context and for its servlets. (kkolinko) Fix: 56665: Correct the generation of the effective web.xml when elements contain an empty string as value. (violetagg) Fix: Fix storeconfig exception routing issues, so that a major problem should avoid configuration overwrite. (remm) Fix: Add configuration fields for header names in SSLValve. (remm) Fix: 56666: When clearing the SSO cookie use the same values for domain, path, httpOnly and secure as were used to set the SSO cookie. (markt) Fix: 56677: Ensure that HttpServletRequest.getServletContext() returns the correct value during a cross-context dispatch. (markt) Fix: 56684: Ensure that Tomcat does not shut down if the socket waiting for the shutdown command experiences a SocketTimeoutException. (markt) Fix: 56693: Fix various issues in the static resource cache implementation where the cache retained a stale entry after the successful completion of an operation that always invalidates the cache entry such as a delete operation. (markt) Fix: When the current PathInfo is modified as a result of dispatching a request, ensure that a call to HttpServletRequest.getPathTranslated() returns a value that is based on the modified PathInfo. (markt) Fix: 56698: When persisting idle sessions, only persist newly idle sessions. Patch provided by Felix Schumacher. (markt) Coyote

Fix: 56663: Fix edge cases demonstrated by ByteCounter relating to data available, remaining and extra write events, mostly occurring with non blocking Servlet 3.1. (remm) Fix: Avoid possible NPE stopping endpoints that are not started (stop shouldn't do anything in that case). (remm) Add: 56704: Add support for OpenSSL syntax for ciphers when using JSSE SSL connectors. Submitted by Emmanuel Hugonnet. (remm) Update: Allow to configure maxSwallowSize attribute of an HTTP connector via JMX. (kkolinko) Jasper

Fix: 56543: Update to the Eclipse JDT Compiler 4.4. (violetagg) Fix: 56652: Add support for method parameters that use arrays and varargs to ELProcessor.defineFunction().(markt) WebSocket

Add: Add support for the permessage-deflate extension. This is currently limited to decompressing incoming messages on the server side. It is expected that support will be extended to outgoing messages and to the client side shortly. (markt) Web applications

Fix: Attempt to obfuscate session cookie values associated with other web applications when viewing HTTP request headers with the Cookies example from the examples web application. This reduces the opportunity to use this example for malicious purposes should the advice to remove the examples web application from security sensitive systems be ignored. (markt) Fix: 56694: Remove references to Manager attribute checkInterval from documentation and Javadoc since it no longer exists. Based on a patch by Felix Schumacher. Also remove other references to checkInterval that are no longer valid. (markt) Other

Update: Update the API stability section of the release notes now that Tomcat 8 has had its first stable release. (markt) Update: Improve build.xml so that when Eclipse JDT Compiler is updated, it will delete the old JAR from build/lib directory. (kkolinko) Code: Simplify implementation of "setproxy" target in build.xml. (kkolinko) Update: Update optional Checkstyle library to 5.7. (kkolinko) Update: 56596: Update to Tomcat Native Library version 1.1.31 to pick up the Windows binaries that are based on OpenSSL 1.0.1h. (markt) Fix: 56685: Add quotes necessary for daemon.sh to work correctly on Solaris. Based on a suggestion by lfuka. (markt) Update: Update package renamed Apache Commons Pool2 to r1609323 to pick various bug fixes. (markt) Update: Update package renamed Apache Commons DBCP2 to r1609329 to pick up a minor bug fix. (markt) Update: Update package renamed Apache Commons FileUpload to r1596086 to pick various bug fixes. (markt) 2014-06-24 Tomcat 8.0.9 (markt)

Catalina

Fix: 55282: Ensure that one and the same application listener is added only once when starting the web application. (violetagg) Fix: 55975: Apply consistent escaping for double quote and backslash characters when escaping cookie values. (markt) Code: 56387: Improve the code that handles an attempt to load a class after a web application has been stopped. Use common code to handle this case regardless of the access path and don't throw an exception purely to log a stack trace. (markt) Code: 56399: Improve implementation of CoyoteAdapter.checkRecycled() to do not use an exception for flow control. (kkolinko) Add: 56461: New failCtxIfServletStartFails attribute on Context and Host configuration to force the context startup to fail if a load-on-startup servlet fails its startup. (slaurent) Add: 56526: Improved the StuckThreadDetectionValve to optionally interrupt stuck threads to attempt to unblock them. (slaurent) Fix: 56545: Pre-load two additional classes, the loading of which may otherwise be triggered by a web application which in turn would trigger an exception when running under a security manager. (markt) Update: 56546: Reduce logging level for stack traces of stuck web application threads printed by WebappClassLoader.clearReferencesThreads() from error to info. (kkolinko) Code: Refactor and simplify common code in object factories in org.apache.catalina.naming package, found thanks to Simian (Similarity Analyser) tool. Improve handling of Throwable. (markt/kkolinko) Fix: Relax cookie naming restrictions. Cookie attribute names used in the Set-Cookie header may be used unambiguously as cookie names. The restriction that prevented such usage has been removed. (jboynes/markt) Fix: Further relax cookie naming restrictions. Version 0 (a.k.a Netscape format) cookies may now use names that start with the $ character. (jboynes/markt) Fix: Restrict cookie naming so that the = character is no longer permitted in a version 0 (a.k.a. Netscape format) cookie name. While Tomcat allowed this, browsers always truncated the name at the = character leading to a mis-match between the cookie the server set and the cookie returned by the browser. (jboynes/markt) Add: Add a simple ServiceLoader based discovery mechanism to the JULI LogFactory to make it easier to use JULI and Tomcat components that depend on JULI (such as Jasper) independently from Tomcat. Patch provided by Greg Wilkins. (markt) Fix: 56578: Correct regression in the fix for 56339 that prevented sessions from expiring when using clustering. (markt) Fix: 56588: Remove code previously added to enforce the requirements of section 4.4 of the Servlet 3.1 specification. The code is no longer required now that Jasper initialization has been refactored and TLD defined listeners are added via a different code path that already enforces the specification requirements. (markt) Fix: 56600: In WebdavServlet: Do not waste time generating response for broken PROPFIND request. (kkolinko) Fix: Provide a better error message when asynchronous operations are not supported by a filter or servlet. Patch provided by Romain Manni-Bucau. (violetagg) Fix: 56606: User entries in tomcat-users.xml file are recommended to use "username" attribute rather than legacy "name" attribute. Fix inconsistencies in Windows installer, examples. Update digester rules and documentation for MemoryRealm. (markt/kkolinko) Coyote

Fix: 56518: When using NIO, do not attempt to write to the socket if the thread is marked interrupted as this will lead to a connection limit leak. This fix was based on analysis of the issue by hanyong. (markt) Fix: 56521: Re-use the asynchronous write buffer between writes to reduce allocation and GC overhead. Based on a patch by leonzhx. Also make the buffer size configurable and remove copying of data within buffer when the buffer is only partially written on a subsequent write. (markt) Fix: Ensure that a request without a body is correctly handled during Comet processing. This fixes the Comet chat example. (markt) Fix: Fix input concurrency issue in NIO2 upgrade. (remm) Fix: Correct a copy/paste error and return a 500 response rather than a 400 response when an internal server error occurs on early stages of request processing. (markt) Code: 56582: Use switch(actionCode) in processors instead of a chain of "elseif"s. (kkolinko) Fix: 56582#c1: Implement DISPATCH_EXECUTE action for AJP connectors. (kkolinko) Fix: Fix CVE-2014-0227: Various improvements to ChunkedInputFilter including clean-up, i18n for error messages and adding an error flag to allow subsequent attempts at reading after an error to fail fast. (markt) Fix: If request contains an unrecognized Expect header, respond with error 417 (Expectation Failed), according to RFC2616 chapter 14.20. (markt) Fix: When an error occurs after the response has been committed close the connection immediately rather than attempting to finish the response to make it easier for the client to differentiate between a complete response and one that failed part way though. (markt) Code: Remove the beta tag from the NIO2 connectors. (remm) Fix: 56620: Avoid bogus access log entries when pausing the NIO HTTP connector and ensure that access log entries generated by error conditions use the correct request start time. (markt) Fix: Improve configuration of cache sizes in the endpoint. (markt) Add: Fix CVE-2014-0230: Add a new limit, defaulting to 2MB, for the amount of data Tomcat will swallow for an aborted upload. The limit is configurable by maxSwallowSize attribute of an HTTP connector. (markt) Jasper

Fix: 56334#c15: Fix a regression in EL parsing when quoted string follows a whitespace. (kkolinko/markt) Update: 56543: Update to the Eclipse JDT Compiler 4.4RC4 to pick up some fixes for Java 8 support. (markt/kkolinko) Fix: 56561: Avoid NoSuchElementException while handling attributes with empty string value. (violetagg) Code: Do not configure a JspFactory in the JasperInitializer if one has already been set as might be the case in some embedding scenarios. (markt) Add: Add a simple implementation of InstanceManager and have Jasper use it if no other InstanceManager is provided. This makes it easier to use Jasper independently from Tomcat. Patch provided by Greg Wilkins. (markt) Fix: 56568: Allow any HTTP method when a JSP is being used as an error page. (markt) Update: 56581: If an error on a JSP page occurs when response has already been committed, do not clear the buffer of JspWriter, but flush it. It will make more clear where the error occurred. (kkolinko) Fix: 56612: Correctly parse two consecutive escaped single quotes when used in UEL expression in a JSP. (markt) Update: Move code that parses EL expressions within JSP template text from Parser to JspReader class for better performance. (kkolinko) Fix: 56636: Correctly identify the required method when specified via ELProcessor.defineFunction(String,String,String,String) when using Expression Language. (markt) Fix: 56638: When using ELProcessor.defineFunction(String,String,String,String) and no function name is specified, use the method name as the function name as required by the specification. (markt) WebSocket

Code: 56446: Clearer handling of exceptions when calling a method on a POJO based WebSocket endpoint. Based on a suggestion by Eugene Chung. (markt) Fix: When a WebSocket client attempts to write to a closed connection, handle the resulting IllegalStateException in a manner consistent with the handling of an IOException. (markt) Fix: Add more varied endpoints for echo testing. (remm) Fix: 56577: Improve the executor configuration used for the callbacks associated with asynchronous writes. (markt) Web applications

Fix: Set the path for cookies created by the examples web application so they only returned to the examples application. This reduces the opportunity for using such cookies for malicious purposes should the advice to remove the examples web application from security sensitive systems be ignored. (markt/kkolinko) Fix: Attempt to obfuscate session cookie values associated with other web applications when viewing HTTP request headers with the Request Header example from the examples web application. This reduces the opportunity to use this example for malicious purposes should the advice to remove the examples web application from security sensitive systems be ignored. (markt) Add: Add options for all of the WebSocket echo endpoints to the WebSocket echo example in the examples web application. (markt) Fix: Ensure that the asynchronous WebSocket echo endpoint in the examples web application always waits for the previous message to complete before it sends the next. (markt) Other

Update: Update package renamed Apache Commons DBCP2 to r1596858. (markt) beta, 2014-05-21 Tomcat 8.0.8 (markt)

Catalina

Fix: 56536: Ensure that HttpSessionBindingListener.valueUnbound() uses the correct class loader when the SingleSignOn valve is used. (markt) Jasper

Fix: 56529: Avoid NoSuchElementException while handling attributes with empty string value in custom tags. Patch provided by Hariprasad Manchi. (violetagg) not released Tomcat 8.0.7 (markt)

Catalina

Fix: 56523: When using SPNEGO authentication, log the exceptions associated with failed user logins at debug level rather than error level. (markt) Coyote

Add: 56399: Assert that both Coyote and Catalina request objects have been properly recycled. (kkolinko) Jasper

Fix: 56522: When setting a value for a ValueExpression, ensure that the expected coercions take place such as a null string being coerced to an empty string. (markt) Other

Fix: Copy missing resources file from Apache Commons DBCP 2 to packaged renamed copy of DBCP 2. (markt) not released Tomcat 8.0.6 (markt)

Catalina

Fix: Fix extension validation which was broken by refactoring for new resources implementation. (markt) Fix: Fix custom UTF-8 decoder so that a byte of value 0xC1 is always rejected immediately as it is never valid in a UTF-8 byte sequence. Update UTF-8 decoder tests to account for UTF-8 decoding improvements in Java 8. The custom UTF-8 decoder is still required due to bugs in the UTF-8 decoder provided by Java. Java 8's decoder is better than Java 7's but it is still buggy. (markt) Fix: 56027: Add more options for managing FIPS mode in the AprLifecycleListener. (schultz/kkolinko) Fix: 56320: Fix a file descriptor leak in the default servlet when sendfile is used. (markt) Fix: 56321: When a WAR is modified, undeploy the web application before deleting any expanded directory as the undeploy process may refer to classes that need to be loaded from the expanded directory. If the expanded directory is deleted first, any attempt to load a new class during undeploy will fail. (markt) Fix: 56327: Enable AJP as well as HTTP connectors to be created via JMX. Patch by kiran. (markt) Fix: 56339: Avoid an infinite loop if an application calls session.invalidate() from the session destroyed event for that session. (markt) Code: 56365: Simplify file name pattern matching code in StandardJarScanner. Improve documentation. (kkolinko) Fix: Ensure that the static resource cache is able to detect when a cache entry is invalidated by being overridden by a new resource in a different WebResourceSet. (markt) Fix: 56369: Ensure that removing an MBean notification listener reverts all the operations performed when adding an MBean notification listener. (markt) Code: Improve implementation of Lifecycle for WebappClassLoader. State is now correctly reported rather than always reporting as NEW. (markt) Add: 56382: Information about finished deployment and its execution time is added to the log files. Patch is provided by Danila Galimov. (violetagg) Add: 56383: Properties for disabling server information and error report are added to the org.apache.catalina.valves.ErrorReportValve. Based on the patch provided by Nick Bunn. (violetagg/kkolinko) Fix: 56390: Fix JAR locking issue with JARs containing TLDs and the TLD cache that prevented the undeployment of web applications when the WAR was deleted. (markt) Fix: Fix CVE-2014-0119: Only create XML parsing objects if required and fix associated potential memory leak in the default Servlet. Extend XML factory, parser etc. memory leak protection to cover some additional locations where, theoretically, a memory leak could occur. (markt) Fix: Modify generic exception handling so that StackOverflowError is not treated as a fatal error and can handled and/or logged as required. (markt) Fix: 56409: Avoid StackOverflowError on non-Windows systems if a file named \ is encountered when scanning for TLDs. (markt) Add: 56430: Extend checks for suspicious URL patterns to include patterns of the form *.a.b which are not valid patterns for extension mappings. (markt) Fix: 56441: Raise the visibility of exceptions thrown when a problem is encountered calling a getter or setter on a component attribute. The logging level is raised from debug to warning. (markt) Add: 56463: Property for disabling server information is added to the DefaultServlet. Server information is presented in the response sent to the client when directory listings is enabled. (violetagg) Fix: 56472: Allow NamingContextListener to clean up on stop if its start failed. (kkolinko) Fix: 56481: Work around case insensitivity issue in URLClassLoader exposed by some recent refactoring. (markt) Add: 56492: Avoid eclipse debugger pausing on uncaught exceptions when tomcat renews its threads. (slaurent) Add: Add the org.apache.naming package to the packages requiring code to have the defineClassInPackage permission when running under a security manager. (markt) Fix: Make the naming context tokens for containers more robust by using a separate object. Require RuntimePermission when introducing a new token. (markt/kkolinko) Fix: 56501: HttpServletRequest.getContextPath() should return the undecoded context path used by the user agent. (markt) Fix: Minor fixes to ThreadLocalLeakPreventionListener. Do not trigger threads renewal for failed contexts. Do not ignore threadRenewalDelay setting. Improve documentation. (kkolinko) Fix: Correct regression introduced in r1239520 that broke loading of users from tomcat-users.xml when using the JAASMemoryLoginModule. (markt) Fix: Correct regression introduced in r797162 that broke authentication of users when using the JAASMemoryLoginModule. (markt) Coyote

Fix: More cleanup of NIO2 endpoint shutdown. (remm) Fix: 56336: AJP output corruption and errors. (remm) Fix: Handle various cases of incomplete writes in NIO2. (remm) Code: Code cleanups and i18n in NIO2. (remm) Fix: Fix extra onDataAvailable calls in the NIO2 connector. (remm) Fix: Fix gather writes in NIO2 SSL. (remm) Code: Upgrade the NIO2 connectors to beta, but still not ready for production. (remm) Code: Fix code duplication between NIO and NIO2. (remm) Fix: 56348: Fix slow asynchronous read when read was performed on a non-container thread. (markt) Fix: 56416: Correct documentation for default value of socket linger for the AJP and HTTP connectors. (markt) Fix: Fix possible corruption if doing keepalive after a comet request. (remm) Fix: 56518: Fix connection limit latch leak when a non-container thread is interrupted during asynchronous processing. (markt) Jasper

Fix: 56334: Fix a regression in the handling of back-slash escaping introduced by the fix for 55735. (markt/kkolinko) Fix: 56425: Improve method matching for EL expressions. When looking for matching methods, an exact match between parameter types is preferred followed by an assignable match followed by a coercible match. (markt) Fix: Correct the handling of back-slash escaping in the EL parser and no longer require that \$ or # must be followed by { in order for the back-slash escaping to take effect. (markt) Cluster

Code: Remove the implementation of org.apache.catalina.LifecycleListener from org.apache.catalina.ha.tcp.SimpleTcpCluster. SimpleTcpCluster does not work as LifecycleListener, it works as nested components of Host or Engine. (kfujino) Fix: Remove cluster and replicationValve from cluster manager template. These instance are not necessary to template. (kfujino) Fix: Add support for cross context session replication to org.apache.catalina.ha.session.BackupManager. (kfujino) Fix: Remove the unnecessary cross context check. It does not matter whether the context that is referenced by other context is set to crossContext=true. The context that refers to the different context must be set to crossContext=true. (kfujino) Code: Move to org.apache.catalina.ha.session.ClusterManagerBase common logics of org.apache.catalina.ha.session.BackupManager and org.apache.catalina.ha.session.DeltaManager. (kfujino) Code: Simplify the code of o.a.c.ha.tcp.SimpleTcpCluster. In order to add or remove cluster valve to Container, use pipeline instead of IntrospectionUtils. (kfujino) Fix: There is no need to set cluster instance when SimpleTcpCluster.unregisterClusterValve is called. Set null than cluster instance for cleanup. (kfujino) WebSocket

Fix: 56343: Avoid a NPE if Tomcat's Java WebSocket 1.0 implementation is used with the Java WebSocket 1.0 API JAR from the reference implementation. (markt) Fix: Increase the default maximum size of the executor used by the WebSocket implementation for call backs associated with asynchronous writes from 10 to 200. (markt) Add: Add a warning if the thread group created for WebSocket asynchronous write call backs can not be destroyed when the web application is stopped. (markt) Fix: Ensure that threads created to support WebSocket clients are stopped when no longer required. This will happen automatically for WebSocket client connections initiated by web applications but stand alone clients must call WsWebSocketContainer.destroy(). (markt) Fix: 56449: When creating a new session, add the message handlers to the session before calling Endpoint.onOpen() so the message handlers are in place should the onOpen() method trigger the sending of any messages. (markt) Fix: 56458: Report WebSocket sessions that are created over secure connections as secure rather than as not secure. (markt) Fix: Stop threads used for secure WebSocket client connections when they are no longer required and give them better names for easier debugging while they are running. (markt) Web applications

Fix: Add Support for copyXML attribute of Host to Host Manager. (kfujino) Fix: Ensure that "name" request parameter is used as a application base of host if "webapps" request parameter is not set when adding host in HostManager Application. (kfujino) Fix: Correct documentation on Windows service options, aligning it with Apache Commons Daemon documentation. (kkolinko) Fix: 56418: Ensure that the Manager web application does not report success for a web application deployment that fails. (slaurent) Update: Improve valves documentation. Split valves into groups. (kkolinko) Fix: 56513: Make the documentation crystal clear that using sendfile will disable any compression that Tomcat may otherwise have applied to the response. (markt) Other

Code: Review source code and take advantage of Java 7's try-with-resources syntax where possible. (markt) Fix: Align DisplayName of Tomcat installed by service.bat with one installed by the *.exe installer. Print a warning in case if neither server nor client jvm is found by service.bat. (kkolinko) Update: 56363: Update to version 1.1.30 of Tomcat Native library. (schultz) Update: Update package renamed Apache Commons BCEL to r1593495 to pick up some additional changes for Java 7 support and some code clean up. (markt) Update: Update package renamed Apache Commons FileUpload to r1569132 to pick up some small improvements (e.g. better null protection) and some code clean up. (markt) Update: Update package renamed Apache Commons Codec to r1586336 to pick up some Javadoc fixes and some code clean up. (markt) Code: Switch to including Apache Commons DBCP via a package renamed svn copy rather than building from a source release for consistency with other Commons packages and to allow faster releases to fix DBCP related issues. (markt) Update: Update package renamed Apache Commons Pool2 and DBCP2 to r1593563 to pick various bug fixes. (markt) Add: In tests: allow to configure directory where JUnit reports and access log are written to. (kkolinko) beta, 2014-03-27 Tomcat 8.0.5 (markt)

Catalina

Fix: Rework the fix for 56190 as the previous fix did not recycle the request in all cases leading to mis-routing of requests. (markt) Fix: Allow web applications to package tomcat-jdbc.jar and their JDBC driver of choice in the web application. (markt) Fix: 56293: Cache resources loaded by the class loader from /META-INF/services/ for better performance for repeated look ups. (markt) Coyote

Fix: Fix possibly incomplete final flush with NIO2 when using non blocking mode. (remm) Fix: Cleanup NIO2 endpoint shutdown. (remm) Fix: Fix rare race condition notifying onWritePossible in the NIO2 HTTP/1.1 connector. (remm) Jasper

Fix: 54475: Add Java 8 support to SMAP generation for JSPs. Patch by Robbie Gibson. (markt) Web applications

Fix: 56273: If the Manager web application does not perform an operation because the web application is already being serviced, report an error rather than reporting success. (markt) Fix: 56304: Add a note to the documentation about not using WebSocket with BIO HTTP in production. (markt) not released Tomcat 8.0.4 (markt)

Catalina

Fix: Restore the ability to use the addURL() method of the web application class loader to add external resources to the web application. (markt) Fix: Improve the robustness of web application undeployment based on some code analysis triggered by the report for 54315. (markt) Fix: 56125: Correctly construct the URL for a resource that represents the root of a JAR file. (markt) Fix: Generate a valid root element for the effective web.xml for a web application for all supported versions of web.xml. (markt) Add: Make it easier for applications embedding and/or extending Tomcat to modify the javaseClassLoader attribute of the WebappClassLoader. (markt) Fix: Add missing support for element when merging web.xml files. (markt) Fix: Improve merging process for web.xml files to take account of the elements and attributes supported by the Servlet version of the merged file. (markt) Fix: Avoid NullPointerException in resource cache when making an invalid request for a resource outside of the web application. (markt) Fix: Remove an unnecessary null check identified by FindBugs. (markt) Add: In WebappClassLoader, when reporting threads that are still running while web application is being stopped, print their stack traces to the log. (kkolinko) Fix: 56190: The response should be closed (i.e. no further output is permitted) when a call to AsyncContext.complete() takes effect. (markt) Fix: 56236: Enable Tomcat to work with alternative Servlet and JSP API JARs that package the XML schemas in such as way as to require a dependency on the JSP API before enabling validation for web.xml. Tomcat has no such dependency. (markt) Fix: 56244: Fix MBeans descriptor for WebappClassLoader MBean. (kkolinko) Add: Add a work around for validating XML documents (often TLDs) that use just the file name to refer to the JavaEE schema on which they are based. (markt) Add: Add methods of get the idle time from last client access time to org.apache.catalina.Session. (kfujino) Fix: 56246: Fix NullPointerException in MemoryRealm when authenticating an unknown user. (markt) Fix: 56248: Allow the deployer to update an existing WAR file without undeploying the existing application if the update flag is set. This allows any existing custom context.xml for the application to be retained. To update an application and remove any existing context.xml simply undeploy the old version of the application before deploying the new version. (markt) Fix: 56253: When listing resources that are provided by a JAR, fix possible StringIndexOutOfBoundsExceptions. Add some unit tests for this and similar scenarios and fix the additional issues those unit tests identified. Based on a patch by Larry Isaacs. (markt) Fix: Fix CVE-2014-0096: Redefine the globalXsltFile initialisation parameter of the DefaultServlet as relative to CATALINA_BASE/conf or CATALINA_HOME/conf. Prevent user supplied XSLTs used by the DefaultServlet from defining external entities. (markt) Coyote

Fix: In some circumstances asynchronous requests could time out too soon. (markt) Fix: 56172: Avoid possible request corruption when using the AJP NIO connector and a request is sent using more than one AJP message. Patch provided by Amund Elstad. (markt) Add: Add experimental NIO2 connector. Based on code developed by Nabil Benothman. (remm) Fix: Fix CVE-2014-0075: Improve processing of chuck size from chunked headers. Avoid overflow and use a bit shift instead of a multiplication as it is marginally faster. (markt/kkolinko) Fix: Fix CVE-2014-0095: Correct regression introduced in 8.0.0-RC2 as part of the Servlet 3.1 non-blocking IO support that broke handling of requests with an explicit content length of zero. (markt/kkolinko) Fix: Fix CVE-2014-0099: Fix possible overflow when parsing long values from a byte array. (markt) Jasper

Fix: Change the default compiler source and compiler target versions to 1.7 since Tomcat 8 requires a minimum of Java 7. (markt) Fix: 56179: Fix parsing of EL expressions that contain unnecessary parentheses. (markt) Fix: 56177: Handle dependency tracking for TLDs when using JspC with a tag library JAR that is located outside of the web application. (markt) Fix: Remove an unnecessary null check identified by FindBugs. (markt) Fix: 56199: Restore validateXml option for JspC which determines if web.xml will be parsed with a validating parser. (markt) Fix: 56223: Throw an IllegalStateException if a call is made to ServletContext.setInitParameter() after the ServletContext has been initialized. (markt) Fix: 56265: Do not escape values of dynamic tag attributes containing EL expressions. (kkolinko) Fix: Make the default compiler source and target versions for JSPs Java 7 since Tomcat 8 requires Java 7 as a minimum. (markt) Update: 56283: Update to the Eclipse JDT Compiler P20140317-1600 which adds support for Java 8 syntax to JSPs. Add support for value "1.8" for the compilerSourceVM and compilerTargetVM options. (markt) WebSocket

Fix: Avoid a possible deadlock when one thread is shutting down a connection while another thread is trying to write to it. (markt) Fix: Avoid NPE when flushing batched messages. (markt) Web Applications

Add: 56093: Add the SSL Valve to the documentation web application. (markt) Fix: 56217: Improve readability by using left alignment for the table cell containing the request information on the Manager application status page. (markt) Fix: Fixed java.lang.NegativeArraySizeException when using "Expire sessions" command in the manager web application on a context where the session timeout is disabled. (kfujino) Fix: Add support for LAST_ACCESS_AT_START system property to Manager web application. (kfujino) Other

Fix: 56115: Expose the httpusecaches property of Ant's get task as some users may need to change the default. Based on a suggestion by Anthony. (markt) Fix: 56143: Improve service.bat so that it can be launched from a non-UAC console. This includes using a single call to tomcat8.exe to install the Windows service rather than three calls, and using command line arguments instead of environment variables to pass the settings. (markt/kkolinko) Code: Simplify Windows *.bat files: remove %OS% checks, as current java does not run on ancient non-NT operating systems. (kkolinko) Fix: Align options between service.bat and exe Windows installer. For service.bat the changes are in --Classpath, --DisplayName, --StartPath, --StopPath. For exe installer the changes are in --JvmMs, --JvmMx options, which are now 128 Mb and 256 Mb respectively instead of being empty. Explicitly specify --LogPath path when uninstalling Windows service, avoiding default value for that option. (kkolinko) Fix: 56137: Explicitly use NIO connector in SSL example in server.xml so it doesn't break if APR is enabled. (markt) Fix: 56139: Avoid a web application class loader leak in some unit tests when running on Windows. (markt) Fix: Correct build script to avoid building JARs with empty packages. (markt) Add: Allow to limit JUnit test run to a number of selected test case methods. (kkolinko) Update: Update Commons Pool 2 to 2.2. (markt) Update: Update Commons DBCP 2 to the 2.0 release. (markt) Fix: 56189: Remove used file cpappend.bat from the distribution. (markt) Fix: 56204: Remove unnecessary dependency between tasks in the build script. (markt) Fix: Add definition of org.apache.catalina.ant.FindLeaksTask. (kfujino) Fix: Implement org.apache.catalina.ant.VminfoTask, org.apache.catalina.ant.ThreaddumpTask and org.apache.catalina.ant.SslConnectorCiphersTask. (kfujino) Add: Add the option to the Apache Ant tasks to ignore the constraint of the first line of the response message that must be "OK -" (ignoreResponseConstraint in AbstractCatalinaTask). Default is false. (kfujino) beta, 2014-02-11 Tomcat 8.0.3 (markt)

Other

Fix: Fix build of Apache Commons DBCP2 classes. (kkolinko) Update: Update Commons DBCP 2 to snapshot 170 dated 07 Feb 2014. This enables DBCP to work with a SecurityManager such that only DBCP needs to be granted the necessary permissions to communicate with the database. (markt) not released Tomcat 8.0.2 (markt)

Catalina

Fix: 56082: Fix a concurrency bug in JULI's LogManager implementation. (markt) Fix: 56085: ServletContext.getRealPath(String) should return null for invalid input rather than throwing an IllegalArgumentException. (markt) Fix: Fix WebDAV support that was broken by the refactoring for the new resources implementation. (markt) Code: Simplify Catalina.initDirs(). (kkolinko) Fix: 56096: When the attribute rmiBindAddress of the JMX Remote Lifecycle Listener is specified it's value will be used when constructing the address of a JMX API connector server. Patch is provided by Jim Talbut. (violetagg) Fix: When environment entry with one and the same name is defined in the web deployment descriptor and with annotation then the one specified in the web deployment descriptor is with priority. (violetagg) Fix: Fix passing the value of false for xmlBlockExternal option of Context to Jasper, as the default was changed in 8.0.1. (kkolinko) Coyote

Fix: Enable non-blocking reads to take place on non-container threads. (markt) Cluster

Code: Simplify the code of o.a.c.ha.tcp.SimpleTcpCluster.createManager(String). Remove unnecessary class cast. (kfujino) Web applications

Fix: In Manager web application improve handling of file upload errors. Display a message instead of error 500 page. Simplify. (kkolinko) Other

Fix: 56104: Correct the version number on the welcome page of the Windows installer. (markt) Update: Update Commons DBCP 2 to snapshot 168 dated 05 Feb 2014. (markt) Fix: Fix CVE-2014-0050, a denial of service with a malicious, malformed Content-Type header and multipart request processing. Fixed by merging latest code (r1565159) from Commons FileUpload. (markt) beta, 2014-02-02 Tomcat 8.0.1 (markt)

Catalina

Fix: Change default value of xmlBlockExternal attribute of Context. It is true now. (kkolinko) Coyote

Fix: Correct regression in the fix for 55996 that meant that asynchronous requests might timeout too early. (markt) Jasper

Fix: Change default value of the blockExternal attribute of JspC task. The default value is true. Add support for -no-blockExternal switch when JspC is run as a standalone application. (kkolinko) WebSocket

Fix: Do not return an empty string for the Sec-WebSocket-Protocol HTTP header when no sub-protocol has been requested or no sub-protocol could be agreed as RFC6455 requires that no Sec-WebSocket-Protocol header is returned in this case. (markt) not released Tomcat 8.0.0 (markt)

Catalina

Add: Implement JSR 340 - Servlet 3.1. The JSR 340 implementation includes contributions from Nick Williams and Jeremy Boynes. (markt) Add: Implement JSR 245 MR2 - JSP 2.3. (markt) Add: Implement JSR 341 - Unified Expression Language 3.0. (markt) Add: Implement JSR 356 - WebSockets. The JSR 356 implementation includes contributions from Nick Williams, Rossen Stoyanchev and Niki Dokovski. (markt) Update: 46727: Refactor default servlet to make it easier to sub-class to implement finer grained control of the file encoding. Based on a patch by Fred Toth. (markt) Add: 45995: Align Tomcat with Apache httpd and perform MIME type mapping based on file extension in a case insensitive manner. (markt) Code: Remove duplicate code that converted a Host's appBase attribute to a canonical file. (markt) Code: 51408: Replace calls to Charset.defaultCharset() with an explicit reference to the ISO-8859-1 Charset. (markt) Code: Refactor initialization code to use a single, consistent approach to determining the Catalina home (binary) and base (instance) directories. The search order for home is catalina.home system property, parent of current directory if boootstrap.jar is present and finally current working directory. The search order for Catalina base is catalina.base system property falling back to the value for Catalina home. (markt) Update: 52092: JULI now uses the OneLineFormatter and AsyncFileHandler by default. (markt) Fix: 52558: Refactor CometConnectionManagerValve so that it does not prevent the session from being serialized in when running in a cluster. (markt) Fix: 52767: Remove reference to MySQL specific autoReconnect property in JDBCAccessLogValve. (markt) Code: Make the Mapper type-safe. Hosts, Contexts and Wrappers are no longer handled as plain objects, instead they keep their type. Code using the Mapper doesn't need to cast objects returned by the mapper. (rjung) Code: Move Manager, Loader and Resources from Container to Context since Context is the only place they are used. The documentation already states (and has done for some time) that Context is the only valid location for these nested components. (markt) Code: Move the Mapper from the Connector to the Service since the Mapper is identical for all Connectors of a given Service and it is common for there to be multiple Connectors for a Service (http, https and ajp). This means there is now only ever one Mapper per Service rather than possibly multiple identically configured Mapper objects. (markt) Code: Remove the per Context Mapper objects and use the Mapper from the Service. This removes the need to maintain two copies of the mappings for Servlets and Filters. (markt) Add: Implement a new Resources implementation that merges Aliases, VirtualLoader, VirtualDirContext, JAR resources and external repositories into a single framework rather than a separate one for each feature. (markt) Add: URL rewrite valve, similar in functionality to mod_rewrite. (remm) Add: Port storeconfig functionality, which can persist to server.xml and context.xml runtime container configuration changes. (remm) Add: 54095: Add support to the Default Servlet for serving gzipped versions of static resources directly from disk as an alternative to Tomcat compressing them on each request. Patch by Philippe Marschall. (markt) Fix: 54708: Change the name of the working directory for the ROOT application (located under $CATALINA_BASE/work by default) from _ to ROOT. (markt) Add: Change default configuration so that a change to the global web.xml file will trigger a reload of all web applications. (markt) Fix: 55101: Make BASIC authentication more tolerant of whitespace. Patch provided by Brian Burch. (markt) Fix: 55166: Move JSP descriptor and tag library descriptor schemas to servlet-api.jar to enable relative references between the schemas to be correctly resolved. (markt) Code: Refactor the descriptor parsing code into a separate module that can be used by both Catalina and Jasper. Includes patches provided by Jeremy Boynes. (violetagg/markt) Code: 55246: Move TLD scanning to a ServletContainerInitializer provided by Jasper. Includes removal of TldConfig lifecycle listener and associated Context properties. (jboynes) Add: 55317: Facilitate weaving by allowing ClassFileTransformer to be added to WebappClassLoader. Patch by Nick Williams. (markt) Fix: 55620: Enable Tomcat to start when either $CATALINA_HOME and/or $CATALINA_BASE contains a comma character. Prevent Tomcat from starting when $CATALINA_HOME and/or $CATALINA_BASE contains a semi-colon on Windows. Prevent Tomcat from starting when $CATALINA_HOME and/or $CATALINA_BASE contains a colon on Linux/FreeBSD/etc. (markt) Code: Initialize the JSP runtime in Jasper's initializer to avoid need for a Jasper-specific lifecycle listener. JasperListener has been removed. (jboynes) Fix: Change ordering of elements of JMX objects names so components are grouped more logically in JConsole. Generally, components are now grouped by Host and then by Context. (markt) Add: Context listener to allow better EE and framework integration. (remm) Fix: 57896: Support defensive copying of "cookie" header so that unescaping double quotes in a cookie value does not corrupt original value of "cookie" header. This is an opt-in feature, enabled by org.apache.tomcat.util.http.ServerCookie.PRESERVE_COOKIE_HEADER system property. (remm/kkolinko) Coyote

Add: Experimental support for SPDY. Includes contributions from Sheldon Shao. (costin) Code: The default connector is now the Java NIO connector even when specifying HTTP/1.1 as protocol (fhanik) Code: Update default value of pollerThreadCount for the NIO connector. The new default value will never go above 2 regardless of available processors. (fhanik) Fix: 54010: Remove some unnecessary code (duplicate calls to configure the scheme as https for AJP requests originally received over HTTPS). (markt) Code: Refactor char encoding/decoding using NIO APIs. (remm) Update: Change the default URIEncoding for all connectors from ISO-8859-1 to UTF-8. (markt) Jasper

Code: Simplify API of ErrorDispatcher class by using varargs. (kkolinko) Code: Update Jasper to use the new common web.xml parsing code. Includes patches by Jeremy Boynes. (markt/violetagg) Add: Create test cases for JspC. Patch by Jeremy Boynes. (markt) Code: 55246: TLD scanning is now performed by JasperInitializer (a ServletContainerInitializer) removing the need for support within the Servlet container itself. The scan is now performed only once rather than in two passes reducing startup time. (jboynes) Fix: 55251: Do not allow JspC task to fail silently if the web.xml or web.xml fragment can not be generated. (markt) Cluster

Code: Remove unused JvmRouteSessionIDBinderListener and SessionIDMessage. (kfujino) Code: Modify method signature in ReplicationValve. Cluster instance is not necessary to argument of method. (kfujino) Code: Remove unused expireSessionsOnShutdown attribute in org.apache.catalina.ha.session.BackupManager. (kfujino) Web applications

Add: Extend the diagnostic information provided by the Manager web application to include details of the configured SSL ciphers suites for each connector. (markt) Update: 48550: Update examples web application to use UTF-8. (markt) Update: 55383: Improve the design and correct the HTML markup of the documentation web application. Patches provided by Konstantin Preißer. (markt) Tribes

Code: Refactor AbstractReplicatedMap to use generics. A key side-effect of this is that the class now implements Map rather than extends ConcurrentMap. (markt) Other

Code: Remove unused, deprecated code. (markt) Code: Remove static info String and associated getInfo() method where present. (markt) Update: (r1353242, r1353410): Remove Ant tasks jasper2 and jkstatus. The correct names are jasper and jkupdate. (kkolinko) Fix: 53529: Clean-up the handling of InterruptedException throughout the code base. (markt) Add: 54899: Provide an initial implementation of NetBeans support. Patch provided by Brian Burch. (markt) Fix: 55166: Move the JSP descriptor and tag library descriptor schema definition files from jsp-api.jar to servlet-api.jar so relative includes between the J2EE, Servlet and JSP schemas are correctly resolved. (markt) Fix: 55372: When starting Tomcat with the jpda option to enable remote debugging, by default only listen on localhost for connections from a debugger. Prior to this change, Tomcat listened on all known addresses. (markt)


#CHANGE LOG ECLIPSE

Subversive Change Log *
*
Subversive - a brand new Eclipse Client for Subversion (SVN) *
See details at http://www.eclipse.org/subversive * ********************************************************************************
Now the Subversive project was moved to Eclipse.org and new version numbers was introduced. Change Log's for older versions still present in this file.

Version 4.0.3.I20161129-1700 [29 November 2016]

Fixes:

Exclude from compare view files with identical content in case they're reported (bug 508237)
Two-way and three-way compare should display "deletion+addition" pairs properly when they're reported instead of "replacement" (bug 508236)
special thanks for the contribution to Florent Angebault
Proper SVNDiffStatus order when deletion and addition are reported for the same nodes (bug 508235)
"Ignore ancestry" option for compare with branch/tag/URL (bug 508231)
special thanks to Florent Angebault
Update from History view and Synchronize view don't change states in another view (bug 505370)
Issue in SVNLightweightDecorator when decorating model elements (resource==null) (bug 502505)
[scalability] Resource listener listens to changes on ignored files (bug 505360)
special thanks for the contribution to Andrey Loskutov
Performance improvements for ResourceStatesChangedEvent (bug 506811)
special thanks for the contribution to Andrey Loskutov
[scalability] SVN update takes hours if "Synchronize" view is opened (bug 504058)
special thanks for the contribution to Andrey Loskutov
Performance improvements for AbstractSVNSubscriber (bug 506777)
special thanks for the contribution to Andrey Loskutov
Performance improvements for SVNUtility (bug 506763)
special thanks for the contribution to Andrey Loskutov
Performance improvements for RemoteStatusCache (bug 506762)
special thanks for the contribution to Andrey Loskutov
Performance improvements for UpdateSubscriber (bug 506760)
special thanks for the contribution to Andrey Loskutov
Performance improvements for FileUtility (bug 506757)
special thanks for the contribution to Andrey Loskutov
Compilation issue with older platform versions (bug 506756)
special thanks for the contribution to Andrey Loskutov
Error in fix for the bug 282000 causes performance issues (bug 506785)
Installation instructions in 'help' are out of date (bug 503327)
Separate requirements page is unnecessary in 'help' (bug 503329)
Remove org.eclipse.team.svn.resource.ignore.rules.jdt bundle (bug 505611)
Correct "management instructions" help page (bug 505119)
Grammar correction on the "Mylyn" help page (bug 505115)
Update Subversive modules overview (bug 505089)
Grammar corrections on the "Supported protocols" page (bug 505006)
Grammar corrections on the "Features" page (bug 504927)
Update Subversive architecture overview (bug 503542)
Linux notes are partially out of date and in need of grammar corrections (bug 503330)
FAQ section in plug-in 'help' requires actualization (bug 503325)
Subversive tries to connect to repository for Compare With -> Base from Working Copy (bug 501030)
Deleting multiple files is very slow on large projects (bug 501032)
Version 4.0.2.I20160902-1700 [02 September 2016]

Fixes:

Documentation is confusing for Merge (bug 487256)
SVN 1.9 requires "local" modifier for status() call in order to work the same way as orevious API versions (bug 500739)
Comparing files from the commit dialog always yields a "no differences" result (bug 497160)
Comparing files from the commit dialog always yields a "no differences" result for unversioned files (bug 500719)
SVN server connection failure with Eclipse Neon (bug 499529)
An error within the SVN+SSH credentials storing code (bug 499333)
ID-UL6V1 History View. Compare current with throws StringIndexOutOfBoundsException (bug 498349)
Background colors for repository nodes in dark theme by default are wrong (bug 499325)
update subversive Icons to fit also dark themes (bug 473419)
Version 4.0.1.I20160719-1700 [19 July 2016]

Fixes:

Accessing SVN Info page leads to error message (bug 497364)
special thanks for the contribution to Gan Ming
Excessive synchronization in SVNUtility class (bug 498026)
SVNMergeHelper does not restore a proper ISVNConnector's state ID-LHNBB
Performance overhead in SVNLightweightDecorator (bug 497139)
SVNLightweightDecorator.isMappedToSVN could fail to recognize if project is connected to SVN (bug 497138)
"ResourceException: Resource 'xyz' is not open" error in decorator (bug 497061)
special thanks for the contribution to Andrey Loskutov
Possible NPE in compare (bug 495959)
special thanks for the contribution to Florent Angebault
Version 4.0.0.I20160604-1700 [04 June 2016]

Fixes:

Resource label is not refreshed in compare panel (bug 493253)
special thanks to Florent Angebault
Reusing compare editor does not refresh changes (bug 495202)
special thanks to Florent Angebault
Not enough debug info when the project is disconnected (bug 495460)
Compare with latest from repository: no changes found when comparing a modified file (bug 495155)
special thanks to Herbert Linseisen
Exception: Resource 'xxx' does not exist ID-NN7GD
Version 4.0.0.I20160427-1700 [27 April 2016]

Fixes:

Incoming addition and deletion statuses are reversed in compare with URL/Revision/Branch/Tag when 1.8 compatible connector is used (bug 492536)
Wrong change direction in compare with URL/Revision/Branch/Tag with 1.8 compatible connectors (bug 492535)
New files and folders aren't displayed in compare with URL/Revision/Branch/Tag when 1.8 compatible connector is used (bug 492534)
Handle peg revision in mergeTwo, diffTwo and diffStatusTwo (bug 492399)
LocateResourceURLInHistoryOperation should use the same code as the one that is used by connectors (bug 492402)
Remove deprecated code related to peg revisions handling (bug 492400)
Version 4.0.0.I20160408-1700 [08 April 2016]

Fixes:

ID-SD9I4 Unable To commit - SVN: '0x0040011a: Call Menu Action' operation finished with error: Argument cannot be null (bug 491153)
Deleted files aren't shown in Synchronize view (bug 491078)
Version 4.0.0.I20160314-1700 [14 March 2016]

Features:

Set SVN Kit 1.8 as default(initial) connector (bug 489643)
Refactor IOptionProvider so that adding another option does not bring an interface change next time (bug 489644)
Add a setting, that allows to commit derived resources (bug 480041)
Need an extension point to provide comment templates programmatically (bug 419093)
Fixes:

SVNRemoteStorage: resource change listener jobs cause OOM (bug 489143)
special thanks to Andrey Loskutov
Ignored files shown as outgoing additions (bug 392750)
Extensive SVN update checks for generated code (bug 489649)
special thanks to Andrey Loskutov
Refactor copy/pasted queue code in SVNRemoteStorage (bug 489664)
Version 4.0.0.I20160226-1700 [26 February 2016]

Features:

SVN Kit 1.8.12: support for Subversion 1.9 new FSFS repository format. (bug 487147)
Parse certificate message passed as parameter by SVN 1.8 and earlier clients in order to provide support for SVN 1.9 API (bug 487220)
"Trust SSL server certificate" dialog should distinguish error codes provided by SVN 1.9 API (bug 488453)
Introduce SVN 1.9 API support (bug 485022)
Enable SVN 1.9 features in SVN 1.9 based connector (bug 488472)
Ensure there is no compatibility issues between plug-in versions with different SVN API supported (bug 488653)
Refactor and remove deprecated merge API calls (bug 488677)
Fixes:

Move 'Create Patch' action in pop-up menu next to 'Apply Patch' (bug 486907)
No content for remote variant of deleted file in Synchronize View (bug 488683)
Version 3.0.4.I20160131-1700 [31 January 2016]

Features:

Make 'Project Structure' preferences page more compact (bug 486862)
SVN Plugin does not provide option to set default checkout directory (bug 486009)
Fixes:

Typo in "Getting Started" documentation (bug 485185)
Information in "Trust server certificate" dialog is hard to read (bug 485344)
"Compare with" dialogs exit with "A path under version control is needed for this operation" error message (bug 485622)
An exception occurs while moving a resource into a package whose SVN text status is set to "Deleted" (bug 486496)
"Inappropriate resource state" exception while adding replaced but not yet added folder to source control (bug 486835)
Version 3.0.3.I20151228-1700 [28 December 2015]

Fixes:

Compare with another branch shows files with no difference SVN 1.7 or older
Weird behavior of the "Compare with branch" feature (bug 484929)
special thanks to Florent Angebault
Deadlock is possible within RelocatedProjectHelper (bug 483402)
Prompt that asks what to do after project relocation shown in a loop forever (bug 482565)
IConnectedProjectInformation is an unneeded interface (bug 483232)
Remove unused code in the InaccessibleLocationDataHelper class (bug 483231)
FindRelatedProjectsOperation should not activate project initialization (bug 483230)
Remove outdated project-to-location management code (bug 483229)
NPE in CreatePatchWizard ID-AW5HY
Unhandled event loop exception org.eclipse.team.svn.ui.panel.local.EditTreeConflictsHelper.getSrcUrl (bug 480521)
Version 3.0.2.I20151028-1700 [28 October 2015]

Features:

Provide interface to use SVN 1.8 diff output options (bug 476177)
Fixes:

NPE in CompareWithLatestRevisionAction ID-D9JJ1
Attempted to beginRule: P/xxxx, does not match outer scope rule in SVNRemoteStorage ID-HTT9T
NPE in SVNRepositoryLocation.asRepositoryContainer ID-W6HFD
Grammatical error (bug 476637)
Unversioned deleted files may reappear in patch dialog if called from Synchronize View (bug 476171)
Version 3.0.1.I20150722-1700 [22 July 2015]

Fixes:

StringIndexOutOfBoundsException in bugtraq in History View (bug 471473)
Reduce I/O amount produced by FileReplaceListener (bug 473193)
Limit SVN status cache refresh depth when possible (bug 473161)
Excessive SVN status reloads for updates, revert, commits etc. (bug 473029)
Improve status cache performance (bug 473028)
Status refresh for files does unnecessary work that significantly reduces performance on large projects (bug 473026)
cant't save file or build waiting for user operation (bug 472752)
Possible resource leak in UI (bug 471963)
If the folder is unversioned, Subversive tries to load it more than once (bug 471205)
Symbolic links and external resources interfere with each other in UI (bug 471204)
There should be a way to add to SVN the intermediate folders produced by svn:externals (bug 471188)
Obstructed externals (bug 465574)
Diff viewer preference page has wrong button sizes in Mars (bug 471161)
Subversive Label Decorations Preferences dialog broken (bug 470990)
Enable team context menu actions on working set (bug 470552)
Version 3.0.0.I20150529-1700 [29 May 2015]

Features:

"set keywords" grayed out for folders (no recursion allowed) (bug 467303)
Fixes:

Improve RefreshResourcesOperation performance (bug 465920)
NullPointerException on SVN history view (JFace plugin) (bug 466983)
ArrayIndexOutOfBoundsException in UpdateSubscriber ID-OJ8UD
NumberFormatException while performing "Synchronize with repository" ID-FE6ZC
File content comparison editor shouldn't be opened for conflicted folders ID-HJ1S2
Version 3.0.0.I20150317-1700 [17 March 2015]

Features:

Refactor SVN API support use strict types for constant enumerations, improve error codes etc.
Update plug-ins API compatibility version (bug 462338)
Update integrations according to API changes (bug 462327)
Fixes:

Useless SVNProperty conversion in AddToSVNWithPropertiesOperation (bug 461199)
Problems using blank spaces for a folder. (bug 459010)
Version 2.0.4.I20150123-1700 [23 January 2015]

Features:

Add typical SVN errors description and possible solutions to help pages (bug 457516)
Fixes:

Can't install Subversive SVN Integration for the M2E Project v2.0.3 (bug 457869)
NPE at CopyRemoteResourcesToWcOperation ID-QI8GK
JRE 1.6 incompatibility ID-HK8DF
Automatic properties do not get applied to new files (bug 456640)
Version 2.0.3.I20141224-1700 [24 December 2014]

Features:

Improve status caching with SVN 1.7/1.8 connectors (bug 449932)
Double click on folders in Compare Editor should expand/collapse them (bug 449598)
There is no way to specify a multi-line property in automatic properties configuration (bug 445999)
Unable to install Subversive via Eclipse Marketplace add "Get Connectors" button into preferences
Move Subversive m2e integration plugin to eclipse.org (bug 455407)
Fixes:

There is a secure storage's password prompt when editing repo props even if the "save password" option is not set (bug 453465)
[KeyBindings] SVN Sync and Commit keybindings no longer work (bug 309074)
Subversive / Maven shortcuts conflict (bug 439499)
[KeyBindings] SVN Sync and Commit keybindings no longer work (bug 309074)
Symlinks treated incorrectly (bug 213197)
Mistake in SVNEntryStatus documentation (bug 452715)
Team->Add to SVN action's enablement is wrong for externally linked resources (bug 452714)
Team->Show History action's enablement is wrong for unversioned resources (bug 452710)
No content for conflicting additions in 3-way compare editor (bug 449601)
Compare editor shouldn't try fetching content of folders as it does for files (bug 449597)
Compare with: Importing new file problem (bug 423308)
FileReplaceListener does not work in Luna (bug 449550)
AddToSVNOperation.removeFromParentIgnore() breaks the "add to SVN" functionality ID-OBDOR
NPE if WorkspaceRoot is passed into FileUtility.getResourcePath() ID-S7NIJ
Automatic properties are processed wrongly when ; or = characters are used as value parts (bug 446000)
In automatic properties configuration dialog only first = should separate name and value (bug 445997)
In automatic properties configuration dialog ; character in a value part should not have a special meaning (bug 445998)
The automatic properties editor validation does not validate the name and the value properly (bug 446001)
Cleanup Subversive-M2E integration's code (bug 456134)
Cancel button is disabled on "Validate Repository Location" progress dialog (bug 455204)
Preserve compatibility with the previous keybindings scheme Default
Version 2.0.1.I20140907-1700 [07 September 2014]

Features:

Refactor Log should be written into console (bug 211245)
Update all SVN operations console output (bug 443135)
Add API to convert SVN command options into command-line counterparts (bug 443132)
Fixes:

There is an exception when unversioned resources selected for synchronizing ID-OX0F5
opening a closed project with svnkit 1.3.8 working copy with JavaHL 1.7 connector freezes Eclipse (bug 440297)
bugtraq:url does not work with URL starting with / (bug 441393)
Create patch with workspace root produces wrong result (bug 437106)
Wrong enablement in Create Patch wizard for nested projects (bug 441039)
FileNotFoundException while trying to save an imported from repository and not existing locally file in "Compare with revision" editor ID-WQB6L
When Project Explorer contains semanticfs then the error "SVN: '0x0040011a: Call Menu Action' operation finished with error: The resource is inaccessible" occurs on commit (bug 437623)
Version 2.0.0.I20140609-1700 [09 June 2014]

Features:

Document SVN API calls (bug 417770)
Fixes:

Refreshing a folder shared with SVN should force Subversive to refresh its state, even if the .svn folder is outside that folder (bug 435601)
Update SVN Cache locks the work space (bug 436727)
Version 2.0.0.I20140519-1700 [19 May 2014]

Fixes:

If performing changes via external program, Subversive does not show actual status (bug 430056)
Delete file from SVN not work always (bug 434944)
Java Refactoring + SVN: Selecting "Cancel" in resource locking dialog leads to empty error dialog (bug 433208)
Version 2.0.0.I20140501-1700 [01 May 2014]

Features:

Add support for Eclipse-SourceReferences header (bug 315011)
special thanks to Michael Schaufelberger
Fixes:

Subversive crashes ID-PPJQ5 (bug 432930)
ArrayOutOfBoundsException in IgnoreMethodPanel ID-MFS28
ResourceException in SaveProjectMetaOperation ID-IE0RW
Subversive produces unnecessary SVN error log entries for eclipse projects. (bug 431237)
A virtual folder in project will cause "The resource is inaccessible" (bug 430349)
Version 2.0.0.I20140309-1700 [09 March 2014]

Features:

Allow freeform in SVN:IGNORE (bug 427577)
Fixes:

Improve bug reporting code in SVNUtility.getWCRoot ID-PH38V
NullPointerException in "Merge properties" (bug 428253)
NPE in EditTreeConflictsPanel ID-LZRIO
Ignored files shown as outgoing additions (bug 392750)
There're unnecessary accesses to the file system while loading information on versioned resources (bug 427184)
There is an exception in Synchronize View when handling an obstructed resource of unexpected kind (dir instead of file) (bug 427183)
GetPropertiesOperation fails for deleted resource with SVN Kit 1.8.3 connector (bug 427093)
SVN 1.7 working copy format detection fails with SVN 1.8.3 connector (bug 427092)
Cannot commit package deletion (greyed out) (bug 426706)
Version 2.0.0.I20131101-1700 [01 November 2013]

Features:

Update SVN operations framework in order to support SVN 1.8 API (bug 423701)
Provide access to SVN repository management API (bug 417769)
Introduce SVN 1.8 API support (bug 417768)
"Treat replacement as edit" should be true by default and should be represented in preferences (bug 419850)
Fixes:

Button position should comply Linux "convention": positive button on the right-most (bug 422826)
NPE in PropertyCompareInput ID-KULS6
Connectors discovery fails with exceptions on MacOS X (bug 418768)
Synchronize view mistakingly treats workspace root as versioned resource ID-NYQUI
FileNotFoundException in FileUtility.copyFile ID-JJCVG
Deleting and replacing a resource is a SVN delete/add instead of a modify (bug 276018)
special thanks to Forest Johnson
Undo Delete result in replaced content (bug 419368)
NPE when using "Create Patch" in history view (bug 419563)
Subversive doesn't allow to use IPv6 addresses as host names (bug 418301)
Version 1.1.1.I20130816-1700 [16 August 2013]

Fixes:

JavaHL Win64 connector isn't shown by the discovery feature (bug 411957)
JavaHL Win32 connector is shown on Win64 platform by the discovery feature (bug 411958)
SVNUtility.getSVNInfo() isn't compatible with SVN 1.7 ID-KOSUR
Copying should be cancelled without getting an error report when destination resource exists on disk but not in sync with workspace ID-IDGZI
OperationCanceledException isn't handled properly (bug 412609)
"Create Patch" wizards show the UTF-8 encoding twice current platform uses UTF-8 by default (bug 414386)
"Create patch" wizard should include each resource into the patch file just once when nested projects are used (bug 414388)
Base revision's content is empty for a file deleted under the SVN 1.7.x client (bug 414400)
"unversioned" string in the ResourceVariant class is not internationalized (bug 414401)
Deleted file's revision is shown incorrectly with SVN 1.7.x client (bug 414406)
Include SVN Kit 1.7.10 version (bug 414897)
Version 1.1.0.I20130527-1700 [27 May 2013]

Fixes:

ClassCastException in time of tag operation (bug 409021)
Repository location: "normalize URL" function does not handle file:/// protocol correctly (bug 409234)
Update switches subfolder back to trunk from branch (bug 406580)
"Apply incoming changes" on "deleted/deleted" generates an error (bug 407631)
When there's a tree conflict, "Edit conflicts" is also enabled and does nothing (bug 407633)
Version 1.0.1.I20130507-1700 [07 May 2013]

Features:

Add "Header" keyword support for svn:keywords property (bug 404239)
Fixes:

Auto lock error with maven hierarchy ID-X5CXN
Compare with base: edits not detected (bug 297717)
Subversive keeps to show incoming changes for files and directories after all incoming changes have been updated (bug 403043)
Sometime annotate fails for files in branches (bug 406726)
"Create Patch" creates patch in UTF-8 (without BOM) irrespective of the file encoding (Windows-1252) (bug 404713)
NPE in SVNRemoteStorage.asRepositoryResource ID-BYM4U
NPE in BuiltInAnnotate ID-IQ1WJ
Enablements of Compare and Replace Actions do not respect ResouceMappings (bug 403200)
Disconnect operation fails when project was unmapped from repository provider prior to disconnect operation ID-LOU8E
NPE in LoggedOperation.setConsoleStream ID-TM2AH
Move ActiveChangeSetManager accessor into the SVN Core plug-in (bug 403980)
Move startup extension into a separate plug-in (bug 403975)
Subversive shows empty post-commit warning window after every commit (bug 402491)
Version 1.0.1.I20130301-1700 [01 March 2013]

Features:

Improvement: add extension point for declaring custom properties (bug 306806)
Set Property dialog should filter/set properties based on resource type (file or folder) (bug 401612)
Display post-commit error messages to the user (bug 354843)
Provide support for post-commit hook's messages (bug 400575)
Improve Team Annotate with useful default revision values (bug 296239)
Fixes:

After modifying properties in "Compare properties" editor, Synchronize View isn't refreshed (bug 401619)
NPE when synchronizing workspace (bug 401898)
Connector install dialog does not open when SVN project exists (bug 401596)
Use the PredefinedProperty class in order to define custom properties (bug 401047)
Move revision properties descriptions into the PredefinedPropertySet class (bug 401041)
Move validation regexp into the PredefinedProperty class (bug 401036)
Use standard internationalization code for a property descriptions (bug 401034)
Add post-commit hook's messages support for 'Mark as Merged' and 'Override and Commit' actions (bug 400583)
Improve annotation UI's performance and usability (bug 400558)
Version 1.0.0.I20130122-1700 [22 January 2013]

Features:

Update JavaHL binaries to 1.7.8 (bug 398671)
Use SVN Kit 1.7.8 (bug 398669)
Fixes:

Spelling error in the method name SVNTeamUIPlugin.getModelC(h)angeSetManager (bug 398654)
Negative revision number exception when all the lines are skipped by SVN annotate ID-I71M1
several texts are not externalized in preference (bug 398261)
Version 1.0.0.I20121228-1700 [28 December 2012]

Features:

Allow to use "Core Configuration Options" extension point (bug 389933)
SVN Connectors failed to install in Eclipse 64 bit for RCP and RAP Developers [Win64 support]. (bug 376317)
Enable error logging for SVN lightweight decorator (bug 395971)
"Clear selection" in the commit dialog unchecks all the items, not only the selected ones (bug 370254)
Human/Numeric ordering option for branches e tags (bug 390467)
Fixes:

Being prompted too aggressively to install SVN connectors (bug 319292)
Charset failure when Applying Patch to a resource (bug 363289)
Got wrong contents for remote file in Subversive (bug 375633)
Text selection extremely slow in C++ editor (bug 350306)
JavaHL connector fails to commit svn:ignore property (bug 395063)
Some tree conflicts caused by merge won't be shown and won't allow user to commit merged changes (bug 395295)
Checkout of a java project from Subversion needs to mangled project name (bug 394761)
Version 1.0.0.I20121109-1700 [09 November 2012]

Features:

Update JavaHL binaries to 1.7.7 (bug 393486)
Use SVN Kit 1.7.6 (bug 393484)
Fixes:

Format code on a source directory with some hundreds of files: takes ages slowed down by SVN change sets
Default change set is not refreshed in the Synchronize View after it is changed (bug 393483)
Mylyn active change set shouldn't be removed automatically when all its changes were moved to another change set (bug 393481)
If Mylyn task is active but empty it does not reappear automatically after IDE restart in SVN change-sets (bug 393480)
Updating an operating system locked file corrupts the project repository (bug 392955)
ampersand in project name (bug 392049)
"Upgrade working copy" action is always disabled for SVN Kit 1.7.5 (bug 393431)
After latest update, icons in synchronize view sometimes not shown (bug 392884)
Version 1.0.0.I20121013-1700 [13 October 2012]

Fixes:

Synchronize window showing add icon decoration instead of delete icon for outgoing change Eclipse 4.2 (bug 388445)
"Edit conflicts" does nothing with a merge conflict caused by properties (bug 390168)
Property change statuses are shown incorrectly when incoming/outgoing deletion is involved (bug 390171)
"Workbench has not been created yet" exception after "out of PermGen space" crash (bug 390177)
"Expand All" is in wrong toolbar group in the "Models" Synchronize View mode (bug 390181)
When working with SVN 1.7-compatible connectors deleted folders are handled improperly (bug 390851)
Moved folder's status is shown wrongly when models support is enabled (bug 390858)
On a repository that is accessed using the file protocol SVN Kit leads to an excessive password prompt (bug 390865)
Resource '...' does not exist exception in AbstractSVNSubscriber ID-GZMNK
Shortcut for "Show Properties" overrides the sign "|" in Slovenian keyboard scheme CTRL+ALT+W -> CTRL+ALT+T
Error when trying to modify a file with the property "svn:needs-lock" in the JSP editor (bug 377013)
Show a user friendly error message if the merge/update/switch caused an unresolved conflict over the .project file ID-UOAA9
Wrong error message text spelling when resources refresh fails
Version 1.0.0.I20120818-1700 [18 August 2012]

Fixes:

Inaccurate preference names and documentation regarding "freeze svn:externals" feature (bug 387324)
Version 1.0.0.I20120803-1700 [03 August 2012]

Fixes:

Edit conflict can not find -right.r file with the SVN 1.7-compatible connectors (bug 383183)
"Check Out As" shouldn't delete an empty project folder, since folder creation later may be impossible due to security restrictions (bug 321810)
[Subversive] - svn:externals syntax check too strict (bug 316114)
Branch/Tag/Copy dialogs should notify about possible ways of "/" character usage (bug 382311)
Refresh on location/root nodes in SVN Repositories View shows multiple credential dialogs (bug 385690)
Unchecked "Save password" repository location option shouldn't prevent user name from being saved (bug 385890)
Using svn+ssh:// repositories with private key authentication causes subversive to popup ssh login dialog two times for every repository operation. (bug 239871)
NPE in FreezeExternalsOperation ID-IP4PU
NPEs in Override and Commit in models mode ID-BOO7P
ClassCastException in time of branch/tag operation ID-M43MD
Version 1.0.0.I20120601-1700 [01 June 2012]

Features:

Graduation release
Version 0.7.9.I20120520-1700 [20 May 2012]

Fixes:

Incorrect console color preferences handling (bug 376929)
NPE in SVNUtility when repository is unavailable ID-S1M7B
Correct supported Eclipse Platform version restriction according to the used API (bug 377864)
"Resource '/.../.svn' does not exist" exception while checking for SVN meta-information ID-BHMBD
NPE while sharing project using the SVN 1.7 connector ID-FMF5P
Version 0.7.9.I20120417-1700 [17 April 2012]

Features:

Create the SVNKit-based SVN 1.7 compatible connector (bug 374582)
Update JavaHL 1.7 connector to the 1.7.4 version
Fixes:

NPE in ScanLocksOperation.createLockFile ID-OKCDI
"Document is closed" exception while writing to the console ID-UODT8
Missing Text fields in Commit dialog (bug 375038)
Version 0.7.9.I20120316-1700 [16 March 2012]

Features:

Add SVN 1.7 support (bug 365627)
Include JavaHL 1.7 connector into the early access/Juno simulatenous release builds (bug 372781)
Fixes:

NPE in EditTreeConflictsPanel due to wrong enablement (bug 373821)
Class SVNConsole shouldn't extend MessageConsole (bug 373049)
SVNConsole class shouldn't be initialized at plug-in startup (bug 370374)
[KeyBindings] SVN Sync and Commit keybindings no longer work (bug 309074)
Commit UI extension fails to set a commit message prior to opening the dialog (bug 372027)
Version 0.7.9.I20120210-1700 [10 February 2012]

Features:

Rename "Commit Templates" preferences node to the "Comments and Input History" (bug 367026)
Smartcard Login on Windows (MSCAPI Support) (bug 351510)
special thanks for the contribution to Markus Oberlassnig (ilogs information logistics GmbH)
Fixes:

org.eclipse.team.svn.ui.compare.ResourceCompareInput.ResourceElement fails to return an InputStream from getContents when compare is invoked against a folder (bug 363845)
If there were no SVN-related activities on the workspace startup, Subversive can't see that imported projects are linked to SVN (bug 336689)
Provide "Edit properties conflicts" to edit conflicts on properties (and mark as merged) (bug 364407)
"Edit Conflicts" action should cover both: property and content conflict cases (bug 370072)
"Mark As Merged" seemingly has no effect on projects with property conflicts (bug 370071)
Exception produced on Show Revision Graph for a source folder (bug 369217)
Move refactoring cause NPE (bug 368325)
Shift and Enter in the commit message window -annoyingly- always causes a commit (bug 366954)
Add "path history depth" setting (bug 367027)
Version 0.7.9.I20111123-1700 [23 November 2011]

Fixes:

There are Eclipse 3.7-specific API usage due to misleading documentation (bug 364572)
Version 0.7.9.I20111119-1700 [19 November 2011]

Features:

Add SVN 1.7 API support (bug 361257)
Replace with Revision fails to notice trivial changes on locked files (bug 353875)
special thanks to Neels Hofmeyr
New decoration mode for branches and tags fullpath
UI commit extensions improvement (bug 356025)
special thanks to Jc Temp
Create patch to Workspace could default location to current project (bug 356042)
IRepositoryLocation state listener (bug 356024)
special thanks to Jc Temp, Eike Stepper
ISVNConnector calls interception API (bug 356023)
special thanks to Jc Temp, Eike Stepper, Adrian
Fixes:

Subversive doesn't refresh synchronize view after commit (bug 329555)
JavaHL: Commit across multiple project atomically does not work (bug 362182)
Collapse All and Expand All buttons are separated in Team Sync view (bug 230868)
"Subversive JDT ignore recommendations" plug-in deadlocks on Eclipse startup (bug 359199)
Problem with RevisionComposite_Reverse (bug 363635)
special thanks to Satoru Yoshida
Problem with MarkAsMergedAction.tooltip (bug 363634)
special thanks to Satoru Yoshida
SVN Compare does not allow new files to be copied (bug 362652)
NPE while obtaining IProxyData data for the specified host ID-ELYHN
If there were no SVN-related activities on the workspace startup, Subversive can't see that imported projects are linked to SVN (bug 336689)
special thanks to Brice Laurencin, Kris De Volder
ClassCastException in ShowHistoryViewOperation ID-L8NW8
Team-private members are marked at wrong time while importing the already shared project (bug 361831)
special thanks to Kris De Volder
There are no notification about the repository node absence while synchronizing workspace (bug 361829)
ReplaceWithRemoteOperation ignores cancellation event (bug 359652)
When updating depth "Recursively" should be the default option (bug 359651)
SVN: '0x00400113: Show Conflict Editor' operation finished with error: null (bug 358998)
FileNotFoundException in ReplaceWithLatestRevisionAction ID-PASE4
Unable to compare files from different branches (bug 356870)
False warning about tag modification (bug 358068)
Create branch from revision not work on project (bug 357562)
NPE in SwitchOperation ID-LK5LW
NPE in ResourceCompareInput ID-H92AC
NPE in MarkAsMergedOperation ID-WZ3PP
Problem during Replace with Latest from repository (temporary path is too long) (bug 297721)
Changes model initialization shouldn't cause an I/O exception ID-AI4E7
Class Preferences, methods savePluginPreferences() and getProxyDataForHost() are deprecated (bug 355996)
Version 0.7.9.I20110819-1700 [19 August 2011]

Features:

Add "record-only" option to the merge dialog (bug 354996)
Fixes:

GetRemoteFolderChildrenOperation implementation depends on the JDK specific (bug 352947)
Do not mess svn:externals order (bug 350143)
special thanks to Julien HENRY
Duplicate folder name for svn:externals if same destination (bug 353009)
special thanks to Julien HENRY
Performance problem with Create Patch (bug 333785)
Refactor SVN locks support code (bug 354058)
Data processing error is mistakenly recognized as a bug in the CreatePatchOperation code ID-W32HV
When i "create patch". The patch file don't encode in utf-8. (bug 284081)
Missing Resources dialog does not resize correctly (bug 304486)
JavaHL is independent of Windows, please properly document this (bug 307397)
Exceptions when eclipse start (bug 302569)
Validation of the issue number using bugtraq:logregex is broken (bug 300402)
SetRevisionAuthorNameOperation shouldn't be performed if original (commit, copy etc.) operation failed ID-WP0UC
Version 0.7.9.I20110715-1700 [15 July 2011]

Features:

Make SVN: 'Save Authorization Info' operation optional (bug 349111)
Update Subversive help regarding persistent SVN+SSH connection option (bug 349139)
Fixes:

Negative revision numbers are not allowed ID-VBVYH
'Replace with revision' fails when using javahl16 connector (bug 351370)
SVN repositories view blocks UI thread (bug 295110)
Useless reordering in the SVN Repositories View (bug 351649)
Team Hook does not work while moving versioned files or folders into unmanaged project (bug 254846)
NPE in CompareEditorInput.setDirty in Eclipse 3.7 ID-MAMS9
SVNKitconnector may access uninitialized CoreExtensionsManager (bug 351357)
IllegalArgumentException in AbstractActionOperation ID-CUA4N
extremely poor refreshLocalResourceImpl performance (bug 259287)
FileReplaceListener performs time consuming actions at inappropriate time (bug 321542)
svn perspective launches svnserve which never close (bug 305658)
Correct french translation for PerformancePreferencePage_enableCache (bug 349138)
Version 0.7.9.I20110602-1700 [2 June 2011]

Fixes:

Correct help section regarding latest changes in Merge Dialog behaviour (bug 347143)
Bug fix: update version number to the actual 1.6.15 (bug 347568)
Indigo requires license update (bug 346698)
Sometimes SVN Kit does not throw an exception when repository is inaccessible ID-VIT54
Version 0.7.9.I20110523-1700 [23 May 2011]

Features:

Provide a flexible way to traverse resources tree in operation execution context (bug 345170)
Fixes:

Deadlock when starting Eclipse with Synch View open ID-V0QM2
Indigo requires license update (bug 346698)
Make revision selection dialog more intuitive (automatically include lesser revision changes into the selected range) (bug 319962)
No way to specify correctly a name for the resources traversal operation (bug 345855)
Rename Class/Interface causes code garbage with Subversive and keyword substitution (bug 315279)
MarkAsMergedOperation ignores cancellation event (bug 345169)
SVNMoveDeleteHook does not report any errors happened while moving resources (bug 344361)
Unused NLS message (bug 343439)
Version 0.7.9.I20110419-1700 [19 April 2011]

Features:

Provide several modes for a branch/tag creation based on the working copy (bug 343073)
Undo and Redo doesn't work in Commit Dialog (bug 298556)
Fixes:

Malformed network data during synchronization (bug 337151) [allow usage of the older SVN Kit version without the issue]
Branch/Tag action from the "Team" menu blocks UI thread (bug 342743)
"Keep resource history" option name in the "Team->Copy To" dialog causes misunderstanding (bug 341723)
Set Keywords action is enabled for new resources (bug 311665)
NPE in SVNHistoryPage resource state listener ID-Q5KRR
Undo Delete does not restore the latest file state but the version before (bug 340318)
Missing NLS string in plugins.properties (bug 341364)
UIMonitorUtility is not equipped to handle applications with more than one shell (bug 341271)
IndexOutOfBoundsException during cache update (bug 315544)
Correct connectors compatibility ID ID-D1U3Y
Version 0.7.9.I20110318-1700 [18 March 2011]

Features:

Add the svn:mergeinfo property into the SVN Property editor list (bug 339832)
Improve bug report facilities (bug 337250)
Fixes:

Correct Mylyn integration feature dependencies (bug 340376)
IllegalStateException in discovery feature when network problem or cancellation occurs ID-FEJWD
Extract operation fails with exception ID-BOAKP
"Unrecognized node kind" error while comparing resources ID-RTYVU
Unhandled EOF exception in Revision Graph EID-NVOHU
No error dialog appears if commit fails (bug 338641)
"Find/Check out as": destination folder browser should open location of actual workspace ID-P1ILO
ResourceContentStorage does not implement equals() (bug 305866)
Update Subversive help regarding installation and updating workflow (bug 338289)
Version 0.7.9.I20110207-1700 [07 February 2011]

Features:

Allow to branch/tag files and folders in single transaction in the SVN Repositories view (bug 335922)
Provide API to open the History view on a specific revision range (bug 335421)
Fixes:

Remove Subversive menu in Help (bug 229495)
The "svnconnector" extension point is broken (bug 336207)
SWTException in SVNTeamModificationValidator when lock is required (bug 336064)
Version 0.7.9.I20110124-1700 [24 January 2011]

Features:

Use the latest SVN Kit version (1.3.5) (bug 334452)
There is no access to the SVN 1.6-related method signatures (bug 333211)
Allow repository creation with the latest SVN Kit-based connector (bug 333202)
Fixes:

Extract operation fails under certain conditions (bug 335079)
Remove duplicated code parts (bug 333061)
Pressing Cancel during compare results in invalid GUI message (no differences) (bug 328820)
Calls to the deprecated function in the SelectPatchFilePage (bug 332775)
There is a compilation issue in the core plug-in under Eclipse 3.7 (bug 332528)
Connectors from polarion update site not detected (bug 328104)
No serialVersionUID for the serializable class ActionIDList (bug 332235)
Finish to create new SVN repository and share project in single operation fails (bug 330780)
Version 0.7.9.I20101203-1700 [03 December 2010]

Fixes:

IWorkspaceRoot.findFilesForLocation() is deprecated (bug 331373)
IWorkspaceRoot.findContainersForLocation() is deprecated (bug 331188)
[ID-ZT6S5] "Negative revision numbers are not allowed" error while performing "Mark As Merged" operation (bug 330737)
Eclipse-LazyStart option is deprecated in Eclipse 3.3 and later versions (bug 331003)
Lots of warnings in the build.properties files (bug 330843)
Use Shell from the FileModificationValidationContext if possible (bug 330638)
Eclipse 3.5 discovery feature connector source code produces compilation errors (bug 330637)
SVNTeamModificationValidator does not take into account LockProposeUtility.proposeLock(..) returned status (bug 330290)
Error in menu item title: "Comapre With" (bug 330228)
Ability to reject incoming changes (make Mark as Merged active) (bug 297821)
Finish button on "Select Resource" dialog not enabled until a different revision is selected (bug 329756)
Correct simple share mode option name (bug 329726)
Wrong French translation for a SVN error (bug 329201)
Some NLS messages should be removed (bug 329187)
SWTException when Subversive UI plugin starts in a worker thread (bug 326684)
No tooltip for clock icon on merge dialog (bug 326074)
NPE starting target workspace (bug 328149)
Properties conflict on project makes Subversive totally unusable. (bug 283999)
Version 0.7.9.I20101001-1700 [01 October 2010]

Fixes:

Update javahl binaries to 1.6.12 version (bug 326829)
Subversive does not start correctly under Eclipse 3.5.x with discovery feature enabled (bug 326834)
Remove SVN 1.4-related connectors from the discovery feature list (bug 326831)
Discovery feature do not starts under Eclipse 3.6 (bug 326564)
Version 0.7.9.I20100917-1700 [17 September 2010]

Features:

Add documentation about Revision Graph options dialog (bug 317802)
[Revision Graph] Allow to hide merge connections by pressing on merge icon (bug 319383)
Make lighter comment color for selected node in Revision Graph (bug 317699)
Allow to call revision graph for multi-selection (bug 318719)
Add help about Properties View contribution in Revision Graph (bug 319109)
Show nodes info in Properties View in Revision Graph (bug 319104)
Show example of date in preferences (bug 299908)
Save revision graph setting in options dialog (bug 317839)
[Revision Graph] Allow to search revision nodes on graph (bug 319968)
[Revision Graph] Allow to specify revisions range (bug 319249)
Support set-depth option (bug 295217)
Fixes:

The conflict editor ignores custom file encoding on the right hand side, uses encoding from container instead (bug 325122)
Resolving Tree Conflicts - Apply Local Changes doesn't work on 2.2.2 (bug 320843)
Subversive should not set forcibly svn:mime-type to text/plain (bug 322772)
NPE in SVNRemoteStorage ID-AFBM0
Default key binding in editors prevents AT from working properly (bug 316097)
Commit Comments history depth doesn't have any effect, when i change it to lower value (bug 302571)
[Revision Graph] Add ... to Show Revision Graph action (bug 319138)
Handle missing resources in Commit dialog (bug 312874)
[Revision Graph] Increase vertical offset between neighbor nodes (bug 319133)
Create patch file filter not working (bug 302937)
[Revision Graph] Increase graph margin (bug 319129)
Error when calling SVN Info for moved resource (bug 315545)
[Revision Graph] Show graph for called resource (bug 319243)
Error in annotation if there are specified revisions (bug 317612)
Connector discovery says it's retrieving list from eclipse.org, but connects to community.polarion.com (bug 320955)
Show History failure - No such revision (bug 312464)
[Revision Graph] Improve comment presentation (bug 319228)
[Revision Graph] Improve tooltip presentation (bug 319148)
Allow to truncate paths in Revision Graph (bug 319029)
Handle if errors happen during revision info fetching at Revision Graph (bug 317801)
NPE in create patch (bug 300720)
Cache directory is empty for revision graph (bug 317266)
All updates in a merge marked as conflicts (bug 312585)
Version 0.7.9.I20100617-1700 [17 June 2010]

Features:

Add merge information to revision graph (bug 313134)
Fixes:

[Show History] Error: Retrieval of mergeinfo unsupported (bug 257669)
Version 0.7.9.I20100528-1600 [28 May 2010]

Fixes:

Lock user account with Subversive (bug 314490)

Realm credentials are not used in auth prompt (bug 314639)

Unable to customize preferences when Subversive is embedded in an eclipse product (bug 311019)

Version 0.7.9.I20100512-1900 [12 May 2010]

Features:

Allow to manage revision graph caches (bug 311015)

Allow to expand/collapse revision nodes (bug 310979)

Provide view with graph of changes: branches, tags etc. (bug 211253)

Correctly support externals in actions (bug 290386)

Fixes:

Invalid action contribution by revision graph (bug 312624)

Add help for revision graph (bug 312562)

SVN Deadlock while trying to open Password Dialog (bug 301417)

SSH settings are not correctly switched in repository locations dialog (bug 310088)

Ssh port not being saved between eclipse restarts (bug 249074)

Make consistent licenses (bug 310430)

org.eclipse.team.svn.ui.lock package isn't exported (bug 310422)

Allow to specify operation id from multiple message bundles (bug 309290)

Error during decoration in Helios M6 (bug 307203)

Subversive Connector Discovery fails on Helios (bug 295156)

Any key binding for rename in SVN Repositories view, should be "F2" (bug 299592)

SVN Workspace Synchronization: Synchronize function does not display proper Icon Decoration for an "Incoming Deletion" (bug 282338)

FileUtility#getPathNodes is inefficient for large change sets (bug 266492)

One slash in URL during Share Project (bug 303085)

Problems when project contains folder called "tags" (bug 303032)

Label for SVN URL changes after restart (bug 298862)

Reintegrate says "No changes found" (bug 297720)

Change bugs title (bug 298574)

Filter JVM Properties when creating Mylyn task (bug 298575)

Compare with branch doesn't work with externals (bug 298573)

Undo after directory move causes irrecoverable data loss (bug 297779)

NPE in getNationalizedString if Localization is not installed (bug 300592)

Can not get Subversive working in I20100122-0800 (bug 300591)

Subversive Connector Discovery fails on Helios M3 (bug 295156)

Subversive is halting the UI (note that jconsole doesn't detect a deadlock, but still it becomes halted) (bug 296707)

NPE in IStateFilter$AbstractStateFilter.accept() (bug 296402)

StackOverflowError when getting authentication info (bug 296689)

File is disappeared from Sync view if update finished with error (bug 295984)

Correctly show files copied with different register case on Windows (bug 295983)

Subversive fails to initialize due to corrupted .svnRepositories file (bug 295954)

dead lock on Linux on startup due to password prompt (bug 295951)

Eclipse UI stalls for more than 5 minutes in the main thread executing SVNRemoteStorage code (bug 296230)

Subversive tries to connect to repository for Compare With -> Base from Working Copy (bug 245326)

Use Equinox secure storage (bug 295079)

Changing svn:ignore on project root directory without updating incoming changes before causes strange behavior (bug 256868)

Support lightweight decorations for Synchronize View (bug 245873)

Start from copy uses trunk instead of branch copy revision (bug 294022)

Problems with locks (bug 294207)

shortcut stops working after first time (bug 293003)

Commit externals problem (bug 290385)

svn:externals definition for a sub-sub-directory breaks after running svn update (bug 270022)

Error during reporting an invalid error (bug 293588)

Make user friendly name for subscriber (bug 293562)

New NLS unused message with latest update (bug 293464)

An empty console window defaults to SVN console (SVN Console should be a console that also display under the opened consoles list) (bug 290797)

Adding file to svn ignore from "Add To SVN Version Control" dialog problem (bug 254902)

An internal error occurred during: "Overwriting 1 resource.". (bug 292577)

Extend SVN Info properties (bug 293016)

NPE when calling Edit Conflicts action (bug 293172)

Make more precise statuses in Commit dialog (bug 293017)

Properties decoration problem (bug 293015)

Version 0.7.8.I20091023-1300 [23 October 2009]

Features:

Add ability to make relative urls in Set External Definition dialog (bug 292674)

Add ability to specify comments for revision links (bug 292280)

Add 'Add Revision Link' action to Team menu (bug 292424)

Provide annotated revision links to save the original revision if switching between trunk and branch (bug 261983)

Add dialog for creating external resource (bug 288139)

In SVN lock view add actions to resources tree (bug 287577)

Fixes:

deadlock in org.eclipse.team.svn.core.SVNTeamPlugin - Eclipse fails to start (bug 291603)

Problems with Set External Definition dialog (bug 292781)

Commit says dir is not part of commit, but it is (bug 292477)

[Subversive] - Bug report ID-L9VHB (bug 254477)

There are no new files in outgoing change sets (bug 292927)

Selection of a single revision to merge results in no changes (bug 287872)

Send Notifications' operation finished with error - repeated dialog (bug 282000)

"Accept" action in the Merge View does not work (bug 289680)

"Edit tree conflicts" action is enablement does not corresponds to what it does (bug 289710)

NPE in SVN Kit 1.3.0 (bug 289812)

"Show History" action from the "Synchronize View" is ineffective (bug 289313)

Merge View incorrectly shows conflicting statuses (bug 289691)

ClassCastException in Override and Update in Merge view (bug 290691)

Trim spaces in repository location (bug 290678)

Add key bindings for Merge action (bug 290718)

Problems with URL field in Merge dialog (bug 290717)

Merge and Synchronize interfered with each other (bug 289689)

Context menu actions in the Merge View does not correctly work (bug 290508)

Change connectors string in SVN Connectors list (bug 290677)

Recommended small change in SVNRemoteStorage.isFileExists() to massively improve performance (bug 291089)

"Local" and "Remote" sub-menus of "Synchronize view" do not appear in my RCP app (bug 290574)

Bad trailing character after french translation "En attente" (bug 274961)

Share Project Wizard dialog typo (bug 264685)

error message when resource location does not match repository location (bug 277787)

Ascendant/Descendant Text Decorations Incorrect (bug 248033)

Synchronize action is hanged (bug 291566)

NPE in SVNRemoteStorage (bug 291580)

NLS unused message (bug 291583)

[Subversive] - "Team -> Switch..." should prefill the input URL with selected resource URL (bug 271297)

Merged files are absent from SVN change Sets (TeamSynchronisation) (bug 282677)

svn externals not working for path/subpath entries (bug 272526)

[Subversive] - Bug report ID-AUVIL (bug 286552)

Preview of merge reintegrate fails (bug 287301)

Support spaces in local path in svn:externals (bug 288107)

Version 0.7.8.I20090904-1300 [04 September 2009]

Features:

Add Capabilities feature

Support reading Subclipse-generated project set files (bug 276947)

Support reading svn-pde-plugin compatible map files (bug 276949)

Connector discovery UI (ala Mylyn) (bug 280889)

List all locked files in a project (bug 279602)

Fixes:

Possible bugs in Subversive Fetch Factory (bug 273230)

Deleting and replacing a resource is a SVN delete/add instead of a modify (bug 276018)

Show annotations does not work in files opened by the XML Editor (bug 267347)

"Compare with Each Other" grayed out (bug 275287)

[Subversive] - Unused NLS Strings for SVN UI (bug 275155)

No assist from "Ignored resources" list. (bug 274793)

RFE: provide Subscriber (bug 272594)

SVNRemoteResourceRevision always returns content of latest revision (bug 271931) Thanks to Steffen Pingel

Attempting to commit files in a folder that has not been added to SVN, locks up Eclipse (bug 251098)

Override and Update deletes all unversioned files disregarding the svn:ignore-list (bug 264500)

A tilde (~) in the repository URL can not be handled (bug 269665)

Concurrent thread access to SVNTeamProvider instance leads to HiddenException (bug 249943)

Usability improvement for repository table in "Checkout from SVN" wizard (bug 263435)

Remember the "Keep Locks" Setting in the Commit Dialog (bug 271742)

[Subversive] - Tip for improvement ID-Q11B5 (Default behaviour of double click in the commit dialog) (bug 257808)

Incorrect previously entered comment in commit dialog (bug 278606)

Handle external definitions in svn commands (bug 255009)

Add ability to specify revision for operations (bug 279083)

Compare with branch/tag doesn't work as expected (bug 279797)

SVN PDE Build uses wrong default path value (bug 279590)

Adding a dated revision link fails (bug 279828)

Selected revisions at bottom of list don't populate Revisions text field in the Merge dialog (bug 279612)

Check Out As Wizard not usable with keyboard. (bug 279355)

cross-project refactoring (bug 281253)

Show History + Export doesn't work (bug 283917)

SelectProjectNamePage (bug 282583)

Error message is incorrect: Window->Preferences->Team->SVN->SVN Client does not exist (bug 281413)

Don't override all revisions in Override and Commit (bug 285138)

NPE after calling Override and Update (bug 283018)

[Subversive] - Incorrect character encoding used for display in Compare view (bug 276138)

Version 0.7.8.I20090506-1500 [06 May 2009]

Features:

Support for files in svn:externals (bug 269155)

Detection of tree conflicts (bug 269156)

Configuration alternative of a diff viewer for MS-WORD documents (bug 260236)

Fixes:

Compare view on right side is empty (bug 272265)

Call commit dialog for svn:externals (for directory) causes error (bug 272025)

svn:externals definition for a sub-sub-directory breaks after running svn update (bug 270022)

All svn:log property values should be normalized to LF endings only (bug 271616)

Create branch doesn't work in Package Explorer (bug 271656)

Synchronize permanently fails with org.eclipse.team.core.TeamException: Resource ?...? does not exist. (bug 267624)

Sorting by user, date or comment does not work for SVN Changeset model in Synchronize view (bug 264331)

SVN Change sets model: Incoming changes are duplicated to a "Unassiged" node (bug 261185)

NPE when activating Mylyn task (bug 266826)

Mylyn Context actions are missing from Team Synchronize view if logical models are enabled (bug 264344)

Synchronization empties outgoing changes if SVN Changesets model is selected (bug 264772)

Version 0.7.7.I20090224-1900 [24 February 2009]

Features:

Add a pre-commit check for files with errors and warnings (bug 263442)

Add ability to output resources comparison in unified diff format (bug 263657)

Add ability to create SVN repository (bug 263951)

Fixes:

Compare with Branches/Tags action problem (bug 263790)

Extract bug (bug 264192)

o.e.team.svn.core has hard dependency to com.ibm.icu bundle (bug 261413)

Bugtraq properties problem (bug 261857)

Problems with relocating project (bug 259626)

Share Projects menu item disabled when multiple projects selected (bug 263003)

Resources list isn't updated in "Override and Update..." (bug 254900)

Add key shortcuts to controls (bug 254726)

Revisions Range dialog isn't correctly resized (bug 261328)

Version 0.7.6.I20081229-1900 [29 December 2008]

Fixes:

Error when trying to create new tag or branch using repository view (bug 259655)
Version 0.7.6.I20081222-1900 [22 December 2008]

Features:

Implement ModelProvider for change sets using IChangeGroupingRequestor (bug 245869)

Implement SVN specific ModelSynchronizeParticipant (bug 245872)

Implement SVN specific SubscriberMergeContext (bug 245870)

Add synchronize pane to commit panel (bug 245874)

Sort changes by status in extract log (bug 255545)

Message Bundles (bug 253520)

Localization - ICU4J (bug 254198)

Fixes:

When extracting only remote changes the conflicted resources are not written to log. (bug 253672)

Extra projects in synchronize view (bug 253887)

Problem with creating a branch/tag (bug 255487)

Subversive deleting unselected and non svn managed files/folders when doing "Override and Update" (bug 251094)

Check out from SVN repository fails when any workspace project uses the RSE file system (bug 230331)

java.util.EmptyStackException in SVNUtility (fetching log entries) (bug 249285)

ClassCastException SVNKit 1.5 getValidReference (bug 252103)

missing "locked message" for a file already locked (bug 247614)

Bug report ID-G6B5P (bug 256949)

Unable to merge: exception when selecting "Revision" radio in merge dialog. (bug 255975)

Creating a patch with a file that does not end with a newline places the "no newline" marker incorrectly (bug 254545)

Tags include trunk subdir (bug 246268)

Version 0.7.5.I20081029-1900 [29 October 2008]

Features:

Browse button in Share dialog (bug 211233)

Allow to select resources only under repository location in Share project's simple mode (bug 249623)

There is no way to type in the repository path when doing a Checkout from SVN (bug 231984)

Add 'Drag and Drop' listeners to the Subversive views (bug 211236)

thanks to Nick Entin for patches
Fixes:

Closing project with file in editor and reopening project generates NPE (bug 246147)

URL decoration with bugtraq properties does not work properly (bug 252563)

Version 0.7.4.I20091001-1900 [01 October 2008]

Features:

Export History log (bug 211415)

thanks to Igor Burilo for the patch
There is no way to type in the repository path when doing a Checkout from SVN (bug 231984)

Allow "override and commit" for non-conflicting resources (bug 241422)

Fixes:

Authentication problems (bug 243914)

Extract from HistoryView fails if the folder has modification and modified children with greater names. (bug 245504)

thanks to Igor Burilo for the patch
Null Pointer Exception in Revision Properties View (bug 248355)

Improve extract log (bug 245509)

Serious usability regression: Replace With merges with revision instead of replacing with revision (bug 240473)

Version 0.7.3.I20080814-1500 [14 August 2008]

Features:

Add date selection options to History View (bug 211408)

special thanks to Gabor Liptak
Allow different behavior for Checkout action (bug 211237)

special thanks to Felipe Carasso, Jacob Robertson
Extract Changes action should not create deletions.log file if no deletions occurs (bug 243395)

Fixes:

butraq:logregex property display disgresses from specification (bug 243678)

special thanks to contributor Jens Scheidtmann
Use standard create patch dialog in Synchronize View (bug 243713)

special thanks to Noah Roberts
getRepository failed: exception AssertionFailedException: null argument (bug 240133)

special thanks to Chomat Stephane
SVN hangs in SVNRepositoryResource.getRoot() method (bug 242130)

special thanks to Neale Upstone
UI pops up dozens of error dialogs making eclipse unusable (bug 220292)

special thanks to David Green
Cannot create a new branch (bug 243181)

special thanks to Jonathan Marston
Synchronize View's Local and Remote submenus are disappeared in Eclipse 3.4 after first call (bug 243045)

special thanks to Noah Roberts, Owen Rees
NPE in Share Project wizard when a project is already exists in the repository (bug 243446)

special thanks to Stephan Heffner
Synchronize doesn't show incomming changes (bug 243401)

special thanks to Tony Poppleton, Channing Walton, Radoslaw Jozwik
Version 0.7.2.I20080801-1500 [1 August 2008]

Features:

When a project is relocated outside Eclipse, and the new URL matches an already-existing repository location, Subversive should automatically update its metadata (bug 231427)

special thanks to Max Bowsher
Improve "Import Project Set" behaviour (bug 230826)

special thanks to Michael Murphree
Provide "Headless" update site (bug 211420)

special thanks to Panagiotis Korros, Thomas Hallgren
decorate working sets in Package Explorer (bug 242249)

special thanks to Igor Fedorenko
Popping up of History View can't be disabled when Compare With action is performed. (bug 242192)

special thanks to Radoslaw Jozwik
Include information about merged revisions into annotation (bug 240156)

Show merged revisions in History View (bug 239819)
Support sparse actions (checkout, import, export) REOPENED
Allow multiple selection for repository operations (export, add revision link). (bug 241249)
Ensure that merge action serves merge-tracking functionality (bug 239818)
Allows to select multiple revisions in merge dialog (bug 239820)
Support merge --reintegrate mode (bug 241500)
Use latest SVN 1.5 binaries REOPENED
Improve "Extract Changes" operation (bug 242557)
Fixes:

ArrayIndexOutOfBoundsException in Create Patch action (bug 242670)

special thanks to Ulli Hafner
Stack overflow while disconnecting a project (bug 241814)

special thanks to Vadim Dmitriev
NPE in MergePanel.getSelection (bug 242753)

special thanks to Igor Fedorenko
New resources are not decorated as outgoing changes (bug 242248)

special thanks to Igor Fedorenko
NPE in MessageDialog (bug 242085)

special thanks to Eugene Babikhin
'Select' button in 'Replace With' window should have a better name (bug 240462)

special thanks to Max Gilead
Replace With -> URL should have better name (bug 240461)

special thanks to Max Gilead
NPE when creating a new project from a repos (bug 242142)

special thanks to Marshall Pierce
NPE while calculating project name before checkout (bug 241777)

special thanks to Wang Lihui
All protocols: Subversive uses incorrect credentials with SVN Kit 1.1.7-based connector (bug 221094)

special thanks to Christopher Smith, Fabio N. Kepler, Antony Jones, Heath Borders, Martin Oberhuber, Jeroen, Nathan Vick, Cinly Ooi
Replace confirmation before main dialog window doesn't make sense (bug 240471)

special thanks to Max Gilead
Merge problem "File not found: revision..." when opening 3-way comparator (bug 240291)

special thanks to Alexey Kamenchuk
"Overwrite and Update" doing merge (bug 237218)

special thanks to Tony Poppleton
Branch from working copy failed with SVN 1.5-compatible connectors (bug 240258)

special thanks to Larry Edelstein
Check out deleted files on my system without asking about it (bug 238916)

special thanks to Vesa Jaaskelainen
Commiting not up to date directory results in uninformative console message only (bug 239105)

special thanks to Max Gilead
Migrate Projects and Settings throws NullPointerException, perhaps on Closed Projects (bug 238863)

special thanks to Brett Randall, Steffen Pingel
view settings wording: contiguous should be incremental (bug 238834)

special thanks to Andrew Bachmann
Properties Configuration preference uses the wrong scrollbars (bug 238389)

special thanks to Kristoffer Peterhansel
Auto-properties not importing from my Subversion config file (bug 238390)

special thanks to Kristoffer Peterhansel
Deadlock when moving multiple sources from one project to another. (bug 233956)

special thanks to Ulli Hafner
SVN replaces files with second last revision after commit (bug 237204)

special thanks to Fabricio Silva
Relocate outside plugin control, then "Share with another repository location" fails (bug 231426)

special thanks to Max Bowsher
NPE in SVN 1.5 compatible connectors when user has no access to repository revision (bug 237408)

special thanks to Darren Hodges
The 'New Working Set' dialog should come up with the default text in the 'Name' textbox already selected (bug 234397)

special thanks to Dan Berindei
NPE in acquireSVNProxy after plug-in is upgraded from the old version (bug 237422)

special thanks to Edward Willink
Share Project should run in background (bug 237304)

special thanks to Lars Vogel
Synchronize View's "Edit Conflicts" action should not touch folders (bug 237264)

special thanks to Markus Dangl
NPE in ClearUpdateStatuses operation (bug 235317)

special thanks to Ulli Hafner
SVNRemoteStorage.asLocalResource() should never return null (bug 216629)

special thanks to Gene Huang
Update help according to plug-in changes (bug 225568)

NPE while refreshing repository browser (bug 240795)
Version 0.7.1.I20080612-1500 [12 June 2008] [build ids are changed corresponding to guidelines]

Features:

Support latest SVN 1.5 API changes (bug 216473)
Fixes:

JavaHLConnector creates a huge amount of short living threads (bug 235764)

special thanks to contributor Micha Riser
Using a proxy server doesn't work (bug 233962)

special thanks to Enrico Ehrich, Francois Masurel
The last added line is ignored in the new file while creating a patch. (bug 236399)

Version 0.7.0.v20080609 [09 June 2008]

Features:

additional date formats for label decorations (bug 217561)

special thanks to Jae Gangemi
special thanks to contributor Thomas Champagne
Revision properties viewer (bug 232728)

Fixes:

Avoid potential deadlock while prompting credentials (bug 236259)
Support Mylyn 3.0 API changes (bug 236100)
NPE in Properties View when "Add" action is called (bug 233407)
Repositories View ignores case sensitivity option (bug 233424)
Version 0.7.0.v20080521 [21 May 2008]

Fixes:

NoClassDefFoundError: org/eclipse/ui/internal/util/SWTResourceUtil (bug 232972)
special thanks to Jorg von Frantzius
Version 0.7.0.v20080517 [17 May 2008]

Features:

Allow to set/modify revision properties (bug 231554)

special thanks to Neale Upstone
Support latest SVN 1.5 API changes REOPENED

Support relative paths and peg-revisions for svn:externals property (bug 231546)
Support sparse checkouts (bug 231552)
Minimize transactions count where it is possible regarding to SVN 1.5 API changes (bug 231548)
Fixes:

NPE in "Replace with Tag" operation (bug 226025)

special thanks to Mark Addleman, Georg Lippold, Chris Myers
Problem with tagging from branches (bug 229761)

special thanks to Damir Murat
Precise Team menu enablements must be disabled by default (bug 230461)

special thanks to Rafael Chaves, Pavel Zuev, Assaf Almaz
Automatic project share makes more than one repository location for the same repository (bug 232649)

Version 0.7.0.v20080425 [25 April 2008]

Fixes:

Feedback on Documentation Page (bug 228692)

special thanks to Nathan Gervais
Attempt to synchronize closed projects produces error (bug 228789)

special thanks to Leo Dos Santos
Mylyn integration won't install due to Mylyn version update to 3.0.0 (bug 228507)

special thanks to Martin Oberhuber
Version 0.7.0.v20080423 [23 April 2008]

Features:

Merge property editor (bug 211411)

special thanks to Francois Fernandes
Enhance copy and move behaviour (bug 227491)

special thanks to Eric Jain
Create M2Eclipse integration plug-in generalized extension point

special thanks to contributor Eugene Kuleshov
Use Quick-Diff annotate for repository files also (bug 228369)

Fixes:

Show Annotations using Quickdiff - Show Author doesn't work (bug 220027)

special thanks to Steve
"Negative revision number" when comparing renamed resources (bug 225972)

special thanks to Jukefox
Team Synchronization very slow (bug 222632)

special thanks to Marc Guenther, Nikolaus Heger
Unable to resolve conflicts (bug 228015)

special thanks to Jesse Eichar
Not asking to save resource before synchronize (bug 224651)

special thanks to Aldo Bongio
Subversive commit key shortcut stops working after first time (bug 225930)

special thanks to Mark Powell
The commit dialog doesn't show the modified files at the top anymore (bug 227136)

special thanks to Paolo
Cleanup plug-in initialization (bug 225884)

special thanks to contributor Eugene Kuleshov
Negative Revision number exception in InfoOperation when SVN Kit is selected (bug 226896)

special thanks to Marijn, Jarkko Lietolahti, Aslam, Steffen Pingel
Incoming change sets are not shown for external resources (bug 227118)

Properties status is not reported while merge. (bug 227102)
Version 0.7.0.v20080404 [04 April 2008]

Features:

Use Eclipse IDE proxy settings (bug 225289)

special thanks to Anders Sveen
Create M2Eclipse integration plug-in (bug 224074)

special thanks to Eugene Kuleshov
Export/Import of repository locations settings (bug 211248)

Rework repository and authentication setting storing. (bug 224616)
Affected path drop-down improvements. (bug 223630)
Update help according to plug-in changes (bug 225568)
Enable Extract for single selection in HistoryView. (bug 223632)
Fixes:

Minimize repository root access (bug 211391)

special thanks to Pavel Zuev
ClassCastException on Override and Update from Synchronize View (bug 224842)

special thanks to Daniel Hirscher, Genady Beryozkin, Edoardo Comar, Leo Dos Santos
Freeze externals uses wrong revision when external reference points to tag or branch without modifications (bug 224597)

special thanks to Marco Perrando
Patch files created under subversive not compatible with patch program REOPENED

special thanks to Mike
Password Management Pref Page improvements (bug 223510)

"Delete" action enablement in Select Resources composite is wrong. (bug 223628)
Enable filter actions for all filtered (History View) (bug 223627)
Some operations can't be sent to background. (bug 223631)
Information about file locker (bug 211254)
Improve Progress Reporting in Composite Operations (bug 223343)
Version 0.7.0.v20080321 [21 March 2008]

Features:

Changed Path filter for history view (bug 222943)
Provide filter management for ILogNode table (bug 222413)
Add drop-down menu to revert dialog. (bug 219983)
Fixes:

Merge changes does not show conflict when file has been renamed (bug 222541)

special thanks to Remi Nodet
Package org.eclipse.team.svn.ui.history.model is not exported (bug 223129)

special thanks to Michael Valenta
Team Synchronization very slow (bug 222632)

special thanks to Marc Guenther
Patch files created under subversive not compatible with patch program (bug 222669)

special thanks to Mike
svn merge view graphical synchronize overwrites changes in local version (bug 221239)

special thanks to Andrew Bachmann, Daniel Hirscher
Advanced merge: Comparison uses empty "Remote File" (bug 220737)

special thanks to Hubert Bildstein
ClassCastException in ShowConflictEditor operation (bug 211390)

Remove Property Editor references. (bug 222388)
Extract improvements (bug 222944)
Synch View Set Property Action bug (bug 223101)
Improve Progress Reporting in Composite Operations (bug 223343)
Update action in Synchronize View performs update to HEAD instead of revision of synchronization (bug 223322)
URL validation is incorrect (bug 223222)
Merge URLs selection dialog should disable revision selection if entered URL is invalid (bug 223221)
Version 0.7.0.v20080311 [11 March 2008]

Fixes:

Fixed incorrect update URL's
Version 0.7.0.v20080307 [07 March 2008]

Features:

Add "Extract Changes..." actions to Synchronize View. (bug 219985)
Add Extract changes action description to Subversive User Guide (bug 221293)
Add "Extract Changes..." action to log messages presentation in History View (bug 220540)
Reuse compare editor when comparing same resource revisions or compare called for revisions from the History View (bug 219628)
Improve History View (new actions in Affected Paths) (bug 218480)
Update JavaHL 1.5.0 connector binaries to alpha2 version (bug 221506)
Fixes:

Compare window opens behind Revert dialog (bug 219775)

special thanks to Steve Streeting
Importing folder from SVN using New Project Wizard - strange behaviour (bug 212746)

special thanks to Michael Spector, Gadi Goldbarg
Check compatibility with Mylyn 2.3.0 task creation API (bug 221498)

The '~' sign is not accepted while defining svn:ignore property (bug 221472)
Revise and simplify History View code (bug 219793)
In Synchronize View operation starts before dialogs (bug 221133)
Properties View has old data, while reading new props. (bug 219572)
Update base table sorter (bug 219583)
Fix images disposing (bug 219455)
Version 0.7.0.v20080218 [18 February 2008]

Fixes:

Change sets on an unavailable Subversive repository disappear (bug 219212)

special thanks to Pim Broekhof
Buttons works incorrectly in history view

Deleted files stay present in synchronize view after commit
NPE when deleting resource inside commit dialog
Invalid date ranges for revision folding in history view
Version 0.7.0.v20080214 [14 February 2008]

Features:

Implement compare and replace actions for branches and tags. (Bug 217553)

special thanks to Andrea Polci
Enhance automatic project share (bug 211399)

special thanks to Max Rydahl Andersen
Two URLs merge mode also should use Merge View (bug 217856)

Add revision folding ability to History view (bug 211410)
Use latest SVN 1.5 binaries (bug 218472)
Open external editor if no built-in editors exists for this file type (bug 218485)
Improve History View (new actions in Affected Paths) (bug 218480)
Add local history to History View (bug 218468)
Fixes:

Team Synchronization reset "remove from view" after each file change (bug 207026)

special thanks to Pawel Piskunowicz
Reported progress is incorrect almost always (it is doubled) (bug 216883)

special thanks to Ilya Klyuchnikov
Conflicts are not shown in Incoming Mode with ChangeSets (bug 189094)

special thanks to Marko Schulz
Some jsp files which have utf-8 encoded characters don't displayed correctly in compare window (bug 211568)

special thanks to YounJung Park
Add warnings for operations, which modify tags. (bug 217844)

special thanks to Edoardo Comar
Replace errors in creating tags and branches with warnings. (bug 217845)

special thanks to Chris Velevitch
java.lang.StackOverflowError when trying to share a new project to SVN (bug 217529)

special thanks to Leo Dos Santos
Replace With > Revision... should mark replaced files dirty (bug 218600)

special thanks to Daniel Hirscher
Problematic configuration in build 20080129 (bug 218647)

special thanks to Alon Peled
Keep ignored resources for "Replace With..." actions (bug 211241)

UI blinks when commit window is called from Package explorer (bug 218136)
Change sets commit fails (NPE) (bug 217291)
Merge two repository browsers for dialogs into one. (bug 217289)
Version 0.7.0.v20080129 [29 January 2008]

Features:

Add "Create patch file" action to the synchronize view drop-down. (bug 216141)

special thanks to Felix Berger
Show conflicting resources in Commit dialog (bug 211404)

special thanks to Gabor Liptak
Allows to override committer name for different protocols (bug 211417)

special thanks to Mark
Allow to select resources for Create Patch action (bug 211413)

special thanks to Kaneider Daniel, Konstantine Kirenko
Add Ignore action to Commit dialog (bug 211407)

Add "Resolve conflicts" and "Mark as merged" actions to Commit dialog (bug 215963)
Add 'Lock" and "Unlock" actions to Commit dialog (bug 215968)
Add "Create patch file" action to Commit dialog (bug 215962)
Add "Replace With" action to Commit dialog (bug 215966)
Add "Compare With" action to a Commit dialog (bug 215964)
"Add to svn:ignore" action in "Add to version control" dialog drop down (bug 216004)
Add "Lock" and "Unlock" actions to synchronize view drop-down menu. (bug 216142)
Add "Show Properties" action to a synchronize view drop down. (bug 216144)
Add "Set properties" and "Set keywords" actions to synchronize view drop-down menu. (bug 216143)
Improve drop-down menu in SynchronizeView (bug 216140)
Improve History View Affected Path Composite drop-down menu. (bug 216264)
Support latest SVN 1.5 API changes (bug 216473)
Fixes:

Commit errors seems to not be shown in console (bug 215188)

special thanks to Kristoffer Peterhansel
It is impossible to install connectors sources on Linux (bug 216699)

special thanks to Ilya Klyuchnikov
"Report revision change" option does not work (bug 216090)

Version 0.7.0.v20080116 [16 January 2008]

Features:

Improve SVN properties support (bug 211403)

special thanks to Olavo Lira
Improve validation in SVN Properties dialog (bug 211402)

Allow to work with non-conflicting resources for "Override and ..." operations (bug 211239)
Implement full tsvn properties support (bug 214894)
Fixes:

Subversive feature not installable from Ganymede Staging Update Site (bug 213975)

special thanks to Markus Knauer
Project migration from polarion to eclipse didn't work (bug 213727)

special thanks to George Lindholm
error when trying to commit with enabled bugtraq properties (bug 214609)

special thanks to Steve Ulrich
Comparing remote files in SVN Repositories view doesn't work (bug 207923)

special thanks to Matthias Erche
Compare: client library returns null value (bug 211260)

special thanks to Samyem
Initial project share to a new repository URL is shared to path "null" under certain circumstances (bug 214839)

special thanks to Daniel M. Zimmerman
Version 0.7.0.v20071221 [21 December 2007]

Fixes:

Subversive 1.1.7 Bugreport broken (bug 204970)

special thanks to Werner Keil
Create Unified Diff action handles direction incorrectly (bug 211272)

special thanks to Artem Tikhomirov
Imporve "Problem Dialog" (bug 211398)

special thanks to Joern Zaefferer
Show the difference between the modified version and the current SVN revision (bug 211250)

SVN 1.5 support changes (bug 213289)
Version 0.7.0.v20071214 [14 December 2007]

Fixes:

Subversive Preferences dialog is substantially too wide (Bug: 212033)

special thanks to Jonathan Amir
Label Decorations preview widget in preferences window is too small (Bug: 212029)

special thanks to Jonathan Amir
bugtraq properties not read for new files (Bug: 211422)

special thanks to Ben Turner
Check compatibility with the Eclipse Ganymede version (Bug: 212732)

tsvn:logminsize is not handled (Bug: 212996)
Version 0.7.0.v20071210 [10 December 2007]

Features:

Spell checking support in Commit dialog and Add/edit commit template is absent (bug 210797)
Fixes:

Rework old-style plug-in manifests (bug 212125)

special thanks to Thomas Hallgren
NPE in SVNRemoteStorage (bug 211392)

special thanks to Mike Price
ClassCastException in LocalShowAnnotationOperation (bug 211275)

special thanks to Frank Bille
Handling % in svn+ssh URLs (bug 211418)

special thanks to Scott Riggins, Jack Newton
CPU hogging (bug 207953)

special thanks to Jorg von Frantzius
GUI hangs (bug 204038)

special thanks to Jappe
classes are packaged in jar files and not in the normal folders structure

special thanks to Alon Peled
Incorrect peg revision used for incoming update on svn:externals resources in Synchronize View (bug 211439)

Make an Hyperlink in the comment clickable (eg. in the history view) (bug 211244)
NPE in Show History (bug 211276)
ArrayIndexOutOfBoundsException in MigrateToEclipse operation (bug 211277)
Attempted to beginRule: P/..., does not match outer scope rule... (bug 211269)
Version 0.7.0.v20071123 [23 November 2007]

Features:

Add "ignore externals" option to "Find/Checkout As" wizard
Fixes:

Port changes in the connection window do not affect the connection (bug 208256)

special thanks to Yaron Mazor
merge UI does not show any changes

special thanks to Chris West
Share Project(s) does not recognize SVN-meta if location with same repository root exists (bug 210683)

Merge UI very slow and fails for projects which names on FS differs in compare to repository (bug 210643)
Error while representing the remote content of the folder with incorrect externals property. (bug 210387)
Rename does not work in SVN Repositories view
ClassCastException is logged when annotating resources from the Synchronize View
Merge UI uses incorrectly encoded URL's (bug 210399)
Compare after refactoring problems (bug 210272)
Fixing issues with "Migrate To Eclipse" action
Add "Migrate to Eclipse" action description into help
build.properties for UI localization plug-in was corrected
SVN client library connector interfaces reworked according to Eclipse guidelines (naming conventions etc.)
switched and svn:externals resources support enhancement
issue in reconstruction URL and PEG pairs from history
incorrect labels in compare UI panels
not encoded URL in AffectedPathsComposite.java
branch operation works incorrectly for multiple project layout when called for working copies
history messages fetched for outgoing changes in context of Incoming Change Set's
file:// and file:/// protocol URL's also should be encoded
support of svn:externals which is not a direct children for the resource on which svn:externals is specified
LocateResourceURLInHistory now works for deleted resources also
incorrect log messages in Change Set mode of merge UI
Mylyn integration refers to incorrect class name
New resources inside new folder does not appear in the Synchronize View
merge UI does not work in "reverse" mode
Enhance compare editor titles readability
Version 1.1.8 [23 October 2007]

Features:

Allow project disconnection from the "Discard Location" dialog (SBV-6187)

special thanks to Scott Harper
Make the history of the entered comments configurable. 5 comments are way too less. (SBV-5832)

special thanks to Paolo Vedovato
Allow checking out projects as folder into nonversioned folders. (SBV-6286)

Allow new resources to be committed into the branch created from the working copy (SBV-6268)
Rework merge UI in order to use standard API's instead of proprietary extensions (SBV-6034)
Add option which enables/disables svn:externals browsing in the SVN Repository Exploring perspective (SBV-5665)
Add decoration on SVN Repositories perspective for resources linked with svn:externals (SBV-5666)
Fixes:

Password prompt is shown time-to-time when svn:externals present even if "save" option specified (SBV-6307)

special thanks to Lira Olavo, CARASSO Felipe
Incompatibility between svn:1.4.3 and svn:1.4.4 working copies (SBV-5630)

special thanks to Fischer
SaveProjectMeta operation copied lot of needless files (SBV-6245)

special thanks to Michal Staruch
Share Projects operation fails with new repository location (SBV-6094)

special thanks to Alexander Wahl (synchronity GmbH)
NPE in Share Projects operation (SBV-6180)

special thanks to Michel, Marko Korhonen
NPE in RepositoryContentProvider when repository is not accessible (SBV-6045)

special thanks to Dennis Vredeveld
Problems with class import when using Subversive API (plug-in is incorrectly packaged) (SBV-6033, bug 204421)

special thanks to Matthias Erche (forum member), Alon Peled, Nikolaos Tsanakas, Yaron Mazor
NPE in HistoryView when it is being initialized (SBV-6063)

special thanks to Jens Gabe, Mark Homan
Messages are shown in Change Set's mode only if Change Set's enabled before synchronize with repository is started (SBV-6032)

special thanks to Vladimir Lapacek (forum member)
Disallow error reporting when status cache load is cancelled (SBV-5877)

special thanks to Belousov Eugeny
"Negative revision number" for quick-diif annotate over empty file (SBV-6314)

Deleted projects detection time-to-time fails (SBV-6311)
Add validation in the plug-in preferences (SBV-6183)
ClassCastException when importing project from SVN (SBV-4513)
Disallow error reporting for SaveProjectMetaOperation (SBV-6113)
ClassCastException if working copy is damaged (SBV-5906)
Exception when hotkey is used without selection (SBV-5944)
svn:externals browse in SVN Repositories view fails if whitespace is present between revision number and revision key (SBV-5943)
Provide user with the correct notification if the selected client library cannot be loaded (SBV-6061)
Version 1.1.7 [23 August 2007]

Features:

Browse svn:externals in SVN Repositories Explorer apply patch
special thanks to contributor Rob Clark
Fixes:

Compare on renamed files fails (bug 188306)

special thanks to Marko Schulz
{Date} tag in label decoration is always showing date in european standard (SBV-5593)

special thanks to George Michelson
Credentials prompt is always shown with the Native JavaHL client (SBV-5625)

Apply SVN Kit client library fixes (SBV-5626)
Problems in the Subversive help plug-in (SBV-5244)
Version 1.1.6 [15 August 2007]

Features:

Move localization into the separate feature (SBV-5562)
Subversive help plug-in improvements (SBV-5244)
Fixes:

[package explorer] Should Collapse MT Parent Packages in Hierarchy Presentation (bug 189976)

special thanks to Adam Cabler, Michael Valenta
Subversion 1.1.5 breaks my PKI usage (SBV-5560)

special thanks to Chris West
Incorrect peg revision specified for "Add Revision Link" action (SBV-5522)

special thanks to Chris West
The "Tip for improvement form" needs work (SBV-3663)

special thanks to Ken Geis
Projects inside Projects not showing incoming changes (SBV-5547)

special thanks to crashedworld (forum member)
Incorrect replacement of file:// to file:/// (SBV-5532)

special thanks to Marcel Albert
Access violation in libsvnjavahl-1.dll (Revert binary to version 1.4.3) (SBV-5449)

special thanks to Carolin Koehler
Repository locations are lost when Eclipse IDE is crashed with "PermGen space: OutOfMemory" error (SBV-5460)

Version 1.1.5 [31 July 2007]

Fixes:

Resources cannot be added to source control with SVN Kit client (SBV-5376)

special thanks to Erik Dick, Mark Smithson, Denis Souza, akg-i,
NPE when synchronizing empty working sets with repository (SBV-5353)

special thanks to Carlo Teubner, Robert Einsle, Lubomir Marinov
Synchronous server access freezes eclipse (SBV-5428)

special thanks to Hans-Christoph Wirth
Create Subversive help plug-in resolving help plug-in issues

"No changes found" message when comparing two files with different names on repository (SBV-5426)
Add to working set does not work when "Find Projects" is selected in the Checkout wizard (SBV-5424)
Invalid radio button selection on the first page of Share Projects wizard (SBV-5420)
Version 1.1.4 [27 July 2007]

Features:

Apply french translation patch sent by Prophessi - SD-mdA (SBV-5291)

special thanks to contributors Prophessi - SD-mdA and Stephane DUCAS, Victoria Anghel, Imed Mami, Sandy Lescaudron
Option to switch off deleted projects detection (SBV-5197)

special thanks to Muchu (forum member)
Adding projects to synchronized working set's (SBV-5198)

special thanks to chrisahn (forum member)
Sort repository locations in the Repositories tree (SBV-5199)

special thanks to chrisahn (forum member)
Create Subversive help plug-in (SBV-5244)

Fixes:

NPE in AbstractSVNTeamAction under Eclipse 3.3 if selection is empty (SBV-5232)

special thanks to Stanislaw Osinski, Mikael Uvebrandt
Command conflict messages under Eclipse 3.3 (SBV-5208)

special thanks to Will Horn
NPE in Show History operation with Native JavaHL client (SBV-5179)

special thanks to Alexey
NPE in Quick-diff based annotation under Eclipse 3.3 (SBV-5183)

NPE in WorkingSetDecorator under Eclipse 3.3 (SBV-5258)
NPE when Show History/Show Annotation called from Synchronize View for deleted file (SBV-5311)
Version 1.1.3 [13 July 2007]

Features:

Add SVN menu and toolbar button (SBV-2501)

special thanks to contributor Rene Link
special thanks to Marcel Schulte, Daniel Winterstein, Bjorn Schorre
Add global shortcut keys for SVN actions (SBV-3494)

special thanks to contributor Rene Link
special thanks to Thomas Bayen, Stig Kleppe-Jorgensen
Support Mylar to Mylyn project name change (SBV-4971)

special thanks to Jim Lombardo, Omry Yadan, Nikola Milutinovic, Kevin Baughman, Antonel Pazargic
Check compatibility with Eclipse 3.3.RC3 IDE (SBV-4973)

Use latest Subversion binaries (SBV-5045)
Use SVN Kit 1.1.2 binaries (SBV-5035)
Use open-source JavaMail version (1.4) (SBV-4986)
Add option to switch off console pattern matcher (SBV-4761)
Fixes:

Usage of disposed font in the History View (SBV-5048)

special thanks to Jorg von Frantzius
Workaround for the deadlock bug in the Eclipse IDE console (194456)

special thanks to Rafael Chaves
Remove the annoying dialog of resource history (Eclipse.org, Bug #188311)

special thanks to Marko Schulz
NPE in SaveProjectMeta operation (SBV-4871)

special thanks to Karl Godel
Zend Technologies patch: fixes deadlock problem in SVNTeamPlugin activation (SBV-4589)

special thanks to Zend Technologies
NPE in SVN Properties when view is disconnected in background thread (SBV-4869)

Negative revision number in Show Annotation operation (SBV-4179)
BadLocationException in "Add hyperlink to console" operation (SBV-4421)
NPE in "Get File Content" operation on files without extensions (SBV-5094)
Cache incorrectly filled after case-sensitive rename on Windows-based platforms (SBV-5100)
Version 1.1.2 [28 April 2007]

Features:

Create Subversive SDK (SBV-4329)

special thanks to Yaron Mazor
Make resources clickable in the SVN Console (SBV-2709)

special thanks to Vladimir Lapacek (forum member)
Fixes:

Speedup Pattern's usage (SBV-4396)

special thanks to contributor Gabor Liptak
peg revisions for compare operation (SBV-4397)

special thanks to contributor Pavel Zuev
ClassCastException in Show History View operation (SBV-4007)

special thanks to Epichler, Volker Berlin, Alessandro Damiani, Bruce Alspaugh, Alan MacKenzie
NPE in Show History View operation (SBV-4088, SBV-4047)

special thanks to Bjorn Voss, Tom Allantonie, Paolo Vedovato, Omry Yadan, J.Ramsdale, Tom Hensel
Widget is disposed exception in History View (SBV-4079, SBV-4374, SBV-4082)

special thanks to Uwe Peuker
NPE in Subversive integration for Mylar (SBV-4380)

special thanks to Thomas Spiessens (forum member)
SVN History implementation does not respect Local History (SBV-4204)

ClientException error code should be copied to ClientWrapperException (SBV-4362)
"Team->Copy To" action does not allow copying into non-versioned folders if "Keep History" is not selected (SBV-4402)
Version 1.1.1 [6 April 2007]

Features:

Integration with Eclipse 3.2 History View (PLC-1111)

special thanks to eu
Revert or delete any file on the commit screen (SBV-2621)

special thanks to Gabor Liptak
Eclipse 3.2 IFileHistoryProvider interface should be implemented (SBV-3886)

special thanks to Armin Bruckhoff
Enhance Mylar integration (SBV-3865)

special thanks to Eugene Kuleshov
Copy/paste from SVN history (SBV-2655)

special thanks to Felipe Carasso
Remove unversioned files while reverting (SBV-3230)

special thanks to Reinhard Brandstaedter
Refine project dependencies (move JDT dependency to extension point)(SBV-2687)

special thanks to Lothar Werzinger, benza (forum member)
Allow users to define --ignore-ancestry option (SBV-3721)

special thanks to mburns (forum member)
Place to specify the SSH port (SBV-2665)

special thanks to Mike De Haan
Proxy tab is missing when non-default client selected (SBV-3720)

special thanks to Benjamin Zeiss
Disable immediate switch while branch/tag from WC if selected resources contains added but not committed resources (SBV-3854)

Fixes:

Share existing projects under Linux rewrites local changes (SBV-3722)

special thanks to Vincent Munier
"Operation is cancelled" dialog. This is a GUI blooper. No dialog like this should come up. (SBV-3714)

special thanks to Adam Kiezun, Omry Yadan
Mark As Merged failure (SBV-3898)

special thanks to A. Fachat, Lars Vogel, Kannky, A. Schmidt
Subversive 1.1.0 with SVN Kit 1.1.1 not working properly with PKI (SBV-3813)

special thanks to Chris West
"Update To" silently reverts all changes (SBV-2418)

special thanks to Hochsteger Andreas (OI&T V)
Incorrect team menu enablement (SBV-3732)

special thanks to Fredy
Widget is disposed exception (SBV-3910)

Projects names are displayed incorrectly while Checkout As with Find project option (SBV-3872)
Set property is not applied recursively to added but not comitted resources (SBV-3916)
Deletion of svn:externals property processed incorrectly (SBV-3936)
Branch/tag misbehaviour (SBV-3961)
Setting svn:ignore property is not reflected properly (SBV-3977)
NPE in History View if project is deleted outside Eclipse IDE (SBV-3987)
NPE while connecting to project with damaged SVN-metainformation (SBV-3990)
Reduce temporary files usage when opening files from repository (SBV-3994)
Version 1.1.0 Release [6 March 2007]

Features:

Externals freezes in TAG (SBV-3698)

special thanks to Olavo Lira, Felipe Carasso
Internationalization. Prepare all string resources to be internationalized (PLC-276)

Fixes:

Wrong internationalization (SBV-3604)

special thanks to Diego Pires Plentz, Martin Gilday, Ken Geis
Subversive seems to be creating extra displays which are unsupported on SWTon GTK (SBV-3691)

special thanks to Michael R. Head
Duplicated objectContribution IDs (SBV-3658)

special thanks to oliviert (forum member)
Conflict editor failed to open (SBV-3711)

"Path is not a working copy directory" error with Native JavaHL client (SBV-3557)
NPE while 'Check out as' with option 'Find projects in the subdirectories of the selected resources' (SBV-3626)
NPE in CheckoutAs Wizard while choosing "Checkout as folder" option and perform finish (SBV-3726)
NPE while repair project's svn meta in "Repair Project" dialog (SBV-3724)
NPE in HistoryView (SBV-3671)
Check out project as folder into existing project misbehaviour (SBV-3625)
Checkout as folder rewrites svn:externals property (SBV-3683)
Branch/Tag from working copy operation creates branch/tag from repository resources (SBV-3692)
Share tracker project action have visual defects + exception in the end (SBV-3499)
Version 1.1.0.RC6 [23 February 2007]

Features:

Text decoration improvments (SBV-3457)

special thanks to contributor Dann Martens
Japanese Localization: apply provided patch (SBV-3598)

special thanks to contributors Takashi Okamoto, Yae Suzuki
Export/Import Subversive preferences: apply provided patch (SBV-3599)

special thanks to contributor Rene Link
Import and Export automatic properties (SBV-3485)

special thanks to Gregory Gerard
Add ability to enter target resource name in "Copy To" action (SBV-3417)

special thanks to Stefan Zeiger
Include SVN Kit 1.1.1 (SBV-3490)

Include latest Subversion binaries (1.4.3) (SBV-3492)
API: Checkout into existing projects like in CVS (PLC-1156)
Fixes:

NPE in Interactive Merge UI (SBV-3537)

special thanks to contributor Rene Link
Checkout into the folder which is a symbolic link failed (SBV-3540)

special thanks to Krystian Nowak
Problems with SVN ignore (SBV-2842)

special thanks to Piet Ritzen
API: Fetching file content in synchronize view is not cancellable (SBV-2867)

special thanks to Adam Kiezun
Allow semicolon-separated properties in "Auto-props" settings (SBV-3506)

special thanks to Gregory Gerard
NPE if synchronize with repository completely failed (SBV-3476)

special thanks to Rostronic
"URL is not related to the repository" for externally relocated projects in RC5 (SBV-3459)

special thanks to Leigh Warren
Subversive does not see command-line svn switch (SBV-3481)

special thanks to irobertson (forum member)
SSH Port Problem (SBV-3434)

special thanks to Nils Grabbert (forum member)
RestoreProjectMetaOperation shouldn't report file system security exceptions (SBV-3483)

special thanks to Valerio Scuderi
Not all temporary files are deleted (SBV-3477)

special thanks to Lukjel
Refactor fails when refactoring one of top packages (SBV-3498)

special thanks to zartc (forum member), cmenzel (forum member), Diego Pires Plentz, Ken Dobson, Richard Musiol
"Cannot non-recursively commit a directory deletion" error with native client (SBV-3497)

special thanks to Paul
"Unrecognized node kind" exception while synchronizing with repository (SBV-3161)

special thanks to Roberto Gonzalez, Ben Christensen, John Francis, Renato Bonomini, Thomas Jachmann
Share multiple projects wizard misbehaviour (SBV-3525)

Repository location URL cannot be changed to non-valid even if no project attached (SBV-3538)
Fetch Content Operation Failure (SBV-3482)
NPE if resources is inaccessible due to some reason (f.e. deleted in background thread) (SBV-3450)
Restore Default Preferences operation cannot be canceled (SBV-3570)
Deleted resources overlay image is not shown if the resource that is scheduled for deletion is external resource (SBV-3583)
All the preferences should be saved in the UI plugin store (SBV-3571)
Version 1.1.0.RC5 [2 February 2007]

Features:

API: Multiple project share required (SBV-2531)

special thanks to Peter M. Murray, Alouf, jtonic, mgcinoz (forum members)
API: Multiple projects merge (SBV-1955)

special thanks to Peter M. Murray, Alouf, jtonic, mgcinoz (forum members)
API: Multiple projects switch (SBV-3398)

special thanks to Peter M. Murray, Alouf, jtonic, mgcinoz (forum members)
Add Open With submenu to HistoryView pop-up menu (SBV-3439)

Fixes:

Allow branching/tagging from Package Explorer even if resources are modified (SBV-3284)

special thanks to Sibylle Peter
Widget is disposed in update operation (SBV-3360)

special thanks to Crumley, Christopher Bradford
Create Patch: at least one revision must be local for a pegged diff (SBV-3406)

special thanks to Adam Kiezun, WhiteFang (forum member)
svn:externals commit behavior (SBV-3433)

special thanks to Lorenzo (forum member)
NPE in Share Project operation (SBV-3271)

Apply Recursively Multiple Properties (SBV-3420)
Export Operation Failure (SBV-3419)
Version 1.1.0.RC4 [20 January 2007]

Features:

API: Improve IMailSettingsProvider extension point (SBV-3234)

special thanks to Bjorn Schorre
Show created report when sending fails (SBV-2615)

special thanks to Ruediger Gubler, Andreas Mayer, Peter Riishoj Brinkler
Add UI for specifying auto-props (like in svn config file) (SBV-3237)

API: Check package layout and refactor if required (SBV-3235)
Fixes:

OutOfMemoryError throwed for very large projects (SBV-3221)

special thanks to Samyem Tuladhar, Leigh Warren
NPE in RemoteStatusOperation (SBV-3275)

special thanks to Paul Kendall
Infinite loop while caching SVN meta-information (SBV-3258)

special thanks to Felipe Carasso, Daniel Hoh, szeiger (forum member), apetrov (forum member), WhiteFang (forum member), Alouf (forum member), jtonic (forum member), asaremba (forum member)
Exception in org.eclipse.team.svn.core.SVNTeamPlugin.start() (SBV-3168)

special thanks to Fabio Zadrozny
404 Not found from time to time (SBV-3175)

special thanks to Robert Einsle
NPE while caching SVN meta-information (SBV-3206)

special thanks to Jon
ActivityCancelledException sometime processed by mail reporter (SBV-3197)

special thanks to Martin Brehm, Dean, rzeznic, Kurt Zettel
NullPointerException in RepositoryPropertiesComposite (SBV-3269)

Merge does not work for resources checked out with svn:externals property (SBV-3236)
Exceptions when file replaced with folder without file deletion committing (SBV-3340)
Team->Set Property action works incorrectly (SBV-3338)
Annotation does not work for incoming additions (SBV-3327)
Team menu does not work properly (SBV-3315)
Version 1.1.0.RC3 [12 January 2007]

Features:

Browse button in the simple mode of the Branch/Tag dialogs (SBV-3149)

special thanks to Alouf (forum member)
Allow quick switch between revisions during compare operation (SBV-1930)

special thanks to Chris Melikian, Francois Fernandes
Support svn:externals property (PLC-445)

special thanks to Bjorn Schorre, Thomas Jachmann, Reinhard Brandstadter, Andreas Boeckler
Add ability to navigate up to parent level in repository browser (SBV-3042)

Fixes:

Excessive work in history view (SBV-3145)

special thanks to contributor Rene Link
Incorrect old SVN clients filtering (SBV-3144)

special thanks to carfield (forum member)
NPE while synchronizing with repository (SBV-3088)

special thanks to Roland Oldenburg
Fix bugtraq integration bug (when bug id is empty) (SBV-3051)

special thanks to contributor Takashi Okamoto
Errors are suppressed in time of commit operation with SVN Kit selected (SBV-2767)

special thanks to Tom Hensel
NPE when svn:externals working copy is damaged (SBV-3173)

Version 1.1.0.RC2 [22 December 2006]

Features:

"Stop revision can not be less than start revision" validation in Merge dialog has no sense (SBV-3030)

special thanks to Judith Burgstein
Allow switch to be performed not only for projects but for folders and files too (SBV-2825)

special thanks to L.Simon
Show versioned resources at the top of the list when doing a commit (SBV-2982)

special thanks to Chris Dail
Integrate Eclipse 3.2 table sorting with our current solution (SBV-2281)

special thanks to Andreas Mayer
Support of BugTraq properties (SBV-1619)

special thanks to Christopher Pierce (forum member)
Make Mylar integration compatible with Mylar 1.0.0 version (SBV-2907)

special thanks to Eugene Kuleshov
Show missing resources status separatelly in the Commit Dialog and warn before update if missing resources was found (SBV-2768)

Show all available information about repository resource in Repository Tree using tooltips (SBV-3022)
Add selected resources count label at the right bottom corner of the commit dialog (SBV-3024)
Fixes:

Change "Subversive" submenu item position in the Eclipse IDE Help menu (SBV-2437)

special thanks to Cristinel Angheluta, Daniel Spiewak
Location is copied after editing its properties (SBV-2940)

Testing and bug fix for the 1.1.0.RC1 Synchronize View (SBV-2937)
NPE in HistoryView on restricted folders (SBV-3009)
Version 1.1.0.RC1 [08 December 2006]

Features:

Paste selected resource names to the commit message in Commit Dialog (SBV-2438)

special thanks to StefanC (forum user)
Add ability to show the immediate parent, direct child of (...) and full path up to root for the tag and branch in the project label (SBV-2805)

special thanks to Dann Martens (contributor), Alouf (forum member)
Allows to select revision manually in "Add Revision Link" dialog (SBV-2785)

special thanks to J S Green (forum member)
Support unified method of multiple and single branch/tag operations (SBV-2074)

special thanks to Thomas Spiessens (forum member), Felipe CARASSO
Include the latest native Subversion binaries and the latest JavaSVN (SVNKit) (SBV-2766)

Make Mylar integration compatible with the latest Mylar version (SBV-2907)
Introduce crash recovery API for the SVN Team Core module (SBV-2856)
Fixes:

New files are added and committed even when they are unchecked (SBV-2803)

special thanks to jmiller (forum member)
Slow down while synchronyzing with repository (SBV-2787)

special thanks to Panagiotis Korros (forum member), Adam Kiezun, afasano (forum member)
FW: SVN History - Compare shows svn rev tag wrong version (SBV-2900)

special thanks to David Koontz, Marco Perrando
NPE in SVNFolderListener (SBV-2875)

special thanks to Laurent Gaches
NPE in Checkout As wizard in case of background project disconnection (SBV-2846)

special thanks to Marcello Ceschia (Univerty of Leipzig)
Excessive repository callbacks after Eclipse restart (SBV-2658)

special thanks to Thomas Feldmann
Get Repository Folder Children operation failure (SBV-2534)

Error when stopping version 1.1.0.M8 (SBV-2714)
Remove leading slashes in the Resource Selection composite (SBV-2831)
SVN Location change unconditionally causes relocate of existing shared projects (PLC-1066)
Content presence detection works incorrectly for single/multiple project layout in Share wizard (SBV-2827)
NPE in Info operation when project is closed/disconnected from source control in background thread (SBV-2889)
NPE while caching resources (SBV-2886)
Version 1.1.0.M9 [17 November 2006]

Features:

Remember size of dialog for comparison of revisions and allow to maximize it (SBV-2725)

special thanks to Andreas Mayer
Enable synchronizing and comparing with previous revisions for the copied files (SBV-2485)

special thanks to Tomas Normark, Nimda Cinatas (forum users)
Contribute SVN Project Reference Analizer for Project Set pligin (SBV-2053)

Fixes:

NPE in Compare operation (SBV-2558)

special thanks to Mark Cooke, Samuel Monsarrat, Pavel, Samant Maharaj, Mark Stralka, Dan Harmer, Patrick, Ignasi Marimon-Clos, Harlan Iverson, Samyem, Stefano Bagnara, Leonid Vasilenko, Barry Kaplan, J. Henne, Dirk, Lee Mercury, Tushar Pokle, B.O.Smievoll, Ben R Vesco, Lars S.-Helldorf
Projects are sometimes disconnected after eclipse restart (SBV-2576)

special thanks to Gordon, Uwe Peuker, Stefan Wurzinger, tom hensel th@macina.com
Initialize Project operation failure (SBV-2628)

special thanks to Michael Goddard
Native JavaHL does not support null as username or password (SBV-2555)

special thanks to Uwe Peuker
NPE in Get Resource List operation Failure Report (SBV-2569, SBV-2570)

special thanks to Lee Mercury, Alex Nistico, A. Antivero, Andy Czerwonka, Euler, Robert Sanders
Share sub-project fails (SBV-2604)

special thanks to Joe Toth
Checking out using New Project Wizard works incorrect (SBV-2536)

special thanks to Arakasi, mortensi (forum users)
svn:ignore does not work in Subversive 1.1.0.M8 (SBV-2550)

special thanks to alexandrupopescu, afasano (forum members), Jon Stevens, Andreas Boeckler
NPE in Share Project operation (SBV-2546)

Compare with revision: IllegalArgumentException: negative revision numbers are not allowed (SBV-2549)
Version 1.1.0.M8 [27 October 2006]

Features:

Support of Subversion 1.4 working copy format (SBV-2450)

special thanks to Ian Rowlands, Stefan Chyssler, Stefan Wurzinger, Tom Hensel
Add file protocol support (SBV-2527)

special thanks to Thorsten Vitt
Improve repository location layout (fonts, coloring, exceeding nodes) (SBV-2519)

special thanks to Pavel Zuev
Allow copying without history for "Copy To" action (SBV-2525)

special thanks to Reinhard Brandstadter
Allow to link History and Property Views with Synchronize Compare editor (SBV-2509)

special thanks to Hubert Grininger
Fixes:

Checking out using New Project Wizard works incorrect (SBV-2536)

special thanks to Arakasi (forum user), Mortensi (forum user)
Define peg revision for actions from Team menu (SBV-2502)

special thanks to Marcel Schulte
Test JavaHL Client usage, fix problems if found (SBV-2406)

Version 1.1.0.M7 [20 October 2006]

Features:

Automatic recognition of repository structure (TRUNK, BRANCHES, TAGS) instead of current static layout (SBV-2389)

special thanks to Diego Ernesto Malpica Chauvet, Felipe Carasso
Respect project repository layout in "Create Branch", "Create Tag" operations (SBV-2388)

special thanks to Diego Ernesto Malpica Chauvet, Felipe Carasso
Compare file on double-click in commit and revert dialogs (SBV-2408)

special thanks to Dario Lopez-Kasten
Show text and property statuses separatelly in the resource selection dialog (PLC-640)

Fixes:

NPE in commit if repository is inaccessible (SBV-2476)

special thanks to Roman Bruggisser, Dario Lopez-Kasten
Add validation to comment view of "Problem Report" and "Tip for Improvement" dialogs (SBV-2498)

special thanks to Hubert Grininger
Incorrect behaviour of "Single Project" layout when sharing project (project shared into branches instead of trunk) (SBV-2445)

special thanks to Kristoffer Peterhansel
Enable checkout of svn:externals (SBV-2497)

special thanks to Hubert Grininger, Reinhard Brandstadter
ClassCastException in experimental merge (SBV-2475)

special thanks to Stas, Alexandre, Andrew Bate, Doug Clinton, Lee Mercury
NPE in Resources Changed operation (SBV-2503)

Version 1.1.0.M6 [13 October 2006]

Features:

Define an option to provide case-sensitive as well as case-insensitive sort (SBV-2363)

special thanks to candyman (forum user)
"expand all" button in synchronize view (SBV-2392)

special thanks to Pavel
Place a splitter into Commit Dialog (SBV-2431)

special thanks to vlp (forum user)
Reconnect projects which metainformation is dropped (PLC-10750)

Add Subversive menu items to the working sets team menu (SBV-2414)
Fixes:

Compare two files from repository shows inverted labels (SBV-2466)

special thanks to Ken Geis
Temporary files should be deleted (SBV-2442)

special thanks to Pavel Zuev
Optimize memory usage and speed up operation performance (PLC-1451)

special thanks to Clint Dovholuk, Daniel Spiewak, Bart Elberg, Richard Vanhook, Samuel Charron, Marvin Toll
NullPointerException in Override and Update for restricted folders (SBV-2447)

SWT error in Annotate View when annotated file is empty (SBV-2448)
'Select All' and 'Deselect All' button work incorrect at resource selection panels (SBV-2446)
NullPointerException in resource selection panel (SBV-2429)
NullPointerException in "Share Project" wizard when "Single Project" layout selected (SBV-2428)
"Access denied" in Override And Update operation (SBV-2424)
Project names are obtained for two times while checkout (SBV-2426)
Version 1.1.0.M5 [29 September 2006]

Features:

Integration with Mylar (PLC-1099)

special thanks to jae (forum member)
Add ability to choose desired revision by hands (not from the list) (SBV-2362)

special thanks to candyman (forum member)
Add ability to create an unified diff on any two revisions (SBV-2364)

special thanks to candyman (forum member)
Provide integration interfaces for Buckminster project (SBV-2412)

Label decorations are not propagated to working sets (PLC-438)
Check out to Working Set (PLC-901)
Allow non-precise menu enablement in case of large projects (SBV-2417)
Fixes:

Compare from Repository View doesn't work on renamed files (SBV-2416)

special thanks to Laszlo Varadi
"Recources Changed" task frequently blinks in the right bottom IDE corner (SBV-2401)

special thanks to Jorg von Frantzius, Dovholuk, Clint
Spelling error in the menu item "Help > Subversive > Send Tip for Improvement" (SBV-2403)

special thanks to Yesudeep J Mangalapilly
JavaSVN reports statuses not only for requested resource but for it parents also Remove debug exception

special thanks to Francois Struman
Unknown node kind exception in time of update operation (SBV-2365)

special thanks to Michael Mauthner
NullPointerException in time of add to SVN operation (SBV-2368)

special thanks to Matias Rodriguez
Poping up project context menu is very slow (PLC-485)

Memory leak in commit dialog (SBV-2397)
Find/Checkout as | Find disabled when called over .polarion folder in polarion project. (SBV-2355)
NullPointerException in interactive merge implementation (SBV-2386)
NullPointerException in time of share project with "multiple" layout selected (SBV-2400)
Version 1.1.0.M4 [15 September 2006]

Features:

Add 'Branch from Revision' and 'Tag from Revision' actions to the History View (SBV-2352)
Fixes:

Problem with specifying user name directly in URL for svn+ssh protocol (SBV-2383)

special thanks to Bronzegraf, reavertm (forum members)
Run Compare Operation in background (SBV-2366)

special thanks to candyman (forum member)
Poping up project context menu is very slow (PLC-485)

Enhance JavaSVN diffStatus() function behavior (SBV-2382)
Version 1.1.0.M3 [8 September 2006]

Features:

Add an ability to edit share project commit message (SBV-2347)

special thanks to bugmenot (forum user)
Open system editors for repository files (SBV-2351)

special thanks to Chris Melikian
Support of the monolitic layout in share operation (SBV-2308)

special thanks to Ken Geis
Support of Quick Diff feature (PLC-1147)

special thanks to Benjamin Pasero
Add 'Link With Editor' button to the History View toolbar (SBV-2325)

special thanks to Adam Brod
Implement built-in annotation like CVS "based on Quick Diff"

Provide ability to send bug report or tip for feature directly from Subversive UI (SBV-2346)
Create 'Password Management' preferences page (SBV-2341)
Create Property View and implement 'Link with Editor' feature for it (SBV-2329)
AnnotationView improvement merge lines with the same revision into on bundle
Fixes:

Deadlock with Subversive Plugin (SBV-2349)

special thanks to rauar (forum user), Michael Valenta
NullPointerException when project is deleted in time of internal cache refresh (SBV-2350)

Version 1.1.0.M2 [1 September 2006]

Features:

Add an ability to choose if double-click opens or compares files in the History View (SBV-2326)
Add 'Compare Current with Revision' menu item to the History View pop-up menu (SBV-2327)
Interrelate items in drop-down menu and toolbar in the History View (SBV-2330)
Fixes:

Apply patch: change wrong "General" tab name to correct "Advanced" in repository settings validation (SBV-2313)

special thanks to contributor Ken Geis
NullPointerException in AbstractDecoratorWrapper (SBV-2312)

Modified resources are not decorated with specified font and colors if they are locked (SBV-2314)
The folder cannot be created in the location root if trunk/branches/tags are disabled (SBV-2315)
'Save password' checkbox is always checked after browsing repository (SBV-2317)
FileNotFoundException while Get Contents action is performed for needs-lock file (SBV-2322)
Version 1.1.0.M1 [23 August 2006]

Features:

Avoid subversive activation when there is no project shared with subversive (SBV-2288)

special thanks to contributor Panagiotis Korros
Commit sets like in CVS (PLC-1097)

special thanks to contributor Alessandro Nistico
Multiple resources properties edit (SBV-2011)

special thanks to Erik (forum user)
Customize resource text colors (PLC-1352)

special thanks to Daniel Spiewak
Add links to "Colors and Fonts" and "Label Decorations" pages on SVN Label Decorations page (SBV-2291)

Improve SVN Console (SBV-2206)
Fixes:

diffStatus() function reports incorrect URL for moved resources (SBV-2248)

special thanks to Adam Brod, Leonardo Barros, BalkanBoy (forum user), vsizikov (forum user)
Plugin doesn't like semicolons in resource names (SBV-2294)

special thanks to Ryan Levering
'Compare with revision' doesn't work for copied/moved resources (SBV-2287)

special thanks to BalkanBoy, vsizikov (forum users)
NullPointerException in CheckoutAs wizard (SBV-2283)

'Needs lock' files cannot be modified right after they are locked by callback (SBV-2289)
Short URL decorator is not correctly displayed in preview (SBV-2290)
Ignored resources are decorated as new (SBV-2293)
Version 1.0.2 [19 August 2006]

Features:

Decorate files which are read-only and need lock (SBV-2226)

special thanks to simas, ftorres (forum users), Chris West
Import from SVN Wizard (PLC-296)

Improve SVN Console (SBV-2206)
Show authentication realm in callback dialog (instead of location URL) (SBV-2236)
Add an ability to represent short url of a project in the package explorer (SBV-2235)
Automatic project share (SBV-2156)
Add 'Checkout subdirectories' option to the checkout wizard (SBV-2216)
Fixes:

Open Repository File operation: NullPointerException in AffectedPathsComposite (SBV-2085)

special thanks to Fabio Frumento
Bug in 1.0.1: Subversive reset editors font settings (SBV-2215)

special thanks to Theo Wilms
Check Out operation: Cannot create a directory (SBV-2200)

special thanks to D. Strauss, Marcus Bitzl, Barry Davies, Marcos Cesar de Oliveira
Update operation: Access denied (SBV-2164)

special thanks to biniobill, Runar Bjarnason
Auto properties support (SBV-2075)

special thanks to Georg (forum member)
Crippling SVN+SSH Bug (SBV-2203)

special thanks to Daniel Spiewak
Get Resource List operation: Unrecognized node kind (SBV-2037)

special thanks to Sandro Orlando, Christian, Jaime Ramos
Show Conflict Editor: ClassCastException while editing conflicts on a *.png files (SBV-2196)

special thanks to Brett Atoms
Check Out operation: Prefix string too short (SBV-2174)

special thanks to Dave Cameron
Improve composite operation performance (SBV-2242)

Project is automatically disconnected while upgrading FastTrack. (SBV-2173)
project share wizard - finish button should be dissabled in FastTrack (SBV-2222)
Merge preview panel becomes gray and empty after resizing (under Eclipse 3.0) (SBV-2237)
Get Resource List: NullPointerException in some complex cases (SBV-2232)
Improve progress monitoring for the operations in the History View and Property Editor (SBV-2218)
checkout projects with its tracker checkouts duplicate projects + project called ".polarion" (SBV-2194)
Malformed SVN console output during Rename Resource (SBV-2209)
Show original SVN "conflict" message when commit fails (SBV-2207)
Check Out operation fails when user checked out projects with the same name but in different case (SBV-2042)
Update does nothing if the project has been switched to the earlier revision (SBV-2034)
IMailSettingProvider has been changed (SBV-2193)
NPE in time of Override And Update operation (SBV-2176)
Version 1.0.1 [28 July 2006]

Features:

SVN Console (SBV-1591)

special thanks to lithium (forum user), dcorbin (forum user), aochsner(forum user), patrek(forum user), markphip(forum user)
Commit/synchronize dialog after share operation (PLC-1421)

special thanks to Daniel Spiewak
Copy change buttons should work in case of compare operations (SBV-1951)

special thanks to Panagiotis Korros
Add an ability to choose the method of project name selection while checkout (SBV-2147)

special thanks to Paul (forum user)
Change File/Class headers with Eclipse standard (SBV-2154)

Moving JavaSVN to extension point (SBV-2135)
Fixes:

Workspace start Problem with IBM RSA 6.0.1.1 and Subversive (SBV-2139)

special thanks to Andreas Graesser
Quick fix for JavaSVN merge() problem (SBV-2158)

special thanks to contributor Tobias Bosch
WTP support: Checkout using new project wizard deletes .settings directory (SBV-2067)

special thanks to angelcervera (forum user)
SVN+SSH: "Unknown authentication method" in JavaSVN SBV-2005

special thanks to CVD (forum user), Anton Fletcher
'Resource does not exist' exception after updating incoming deletion (SBV-2171)

[Subversive] Report ID-Y6AUL - Import Team Project Set Operation Failure Report (SBV-2137)
Invalid thread access (SBV-2127)
Version 1.0.0 Release [14 July 2006]

Features:

Enhance Add/Edit properties (SBV-2065)

special thanks to wusch (forum user)
Support of different merge modes (SBV-2069)

special thanks to yagee (forum user)
Add an ability to apply lock to the resourses recursively (SBV-2097)

Support conflicitng files editing (SBV-2079)
Implement standard JavaHL merge (SBV-2098)
Fixes:

Incorrect URL when only one file is merged (SBV-2101)

special thanks to Danny Mandel
NPE while synchronizing projects (SBV-2091)

special thanks to Kevin Ross, biniobill
Share Project operation: Negative revision number (SBV-2061)

special thanks to Chad Woolley
Bug in synchronize view after merge (SBV-1949)

special thanks to Clint Dovholuk
Can't relocate a project (SBV-2076)

special thanks to smonsarr (forum user)
Compare operation fails in complex case (SBV-2118)

special thanks to J.J. Kiers
WTP support: Checkout using new project wizard deletes .settings directory (SBV-2067)

special thanks angelcervera (forum user)
Strange strings in decorators preference page (SBV-2064)

special thanks Panagiotis Korros
reduces memory consumption by 15% (SBV-2103)

special thanks to contributor Panagiotis Korros for provided patch
.svn folder is deleted by subversive (SBV-2102)

special thanks to contributor Panagiotis Korros for provided patch
NullPointerException in Annotate View (SBV-1818)

special thanks to Sébastien Sahuc
Enable Finish button on Share project (SBV-2056)

Revision '-1' is set to added resources in property editor title (SBV-2095)
NullPointerException in Get Remote Properties operation (SBV-2060)
Repository Browser decoration is not refreshed after 'Break lock' action (SBV-2072)
Checkout using 'New Project Wizard' should not suggest to overwrite existing project (SBV-2071)
Selecting repository location label works incorrect (SBV-2070)
Incomplete presentation of project URL's in 'Find / Checkout Projects As' wizard (SBV-2078)
'Start development with' option for branch/tag actions doesn't work sometimes (SBV-2073)
Override and update doesn't work for new resources (SBV-2096)
NullPointerException in Add to SVN operation (SBV-1921)
Cannot change credentials for svn+ssh protocol (SBV-2115)
JavaSVN features (in cooperation with TMate team):

Add "force" option to SVNClientEx::merge() function (SBV-2049)
Version 1.0.0 RC4 [30 June 2006]

Features:

Enhance properties support (SBV-1784)

special thanks to Erik (forum user)
Add menu item 'Add Revision Link' to the History View (SBV-2032)

Add getSelectedLogMessages() method to SelectRevisionPanel class (SBV-2038)
Add error and warning decoration to the resources in commit dialog (SBV-2059)
Add an ability to choose if the new resources should be selected in commit dialog or not (SBV-2058)
Fixes:

Problem adding property names with more than 1 ':' character. (SBV-2014)

special thanks to Alexis O'Connor
Set focus to password field when callback dialog is shown (SBV-2012)

special thanks to Chris West
ResourceException: A resource exists with a different case (SBV-2040)

special thanks to Maarten Meijer
Some entry fields information is not correctly passed to the operations (SBV-2013)

Create folder operation fails for the folders which are repository roots (SBV-2021)
'Widget disposed error' after dialog is closed by 'Esc' and 'Ctrl+Enter' is pressed (SBV-2022)
Affected paths tree does not contain statuses information for some folders (SBV-2023)
Cannot create branch in the root of repository (SBV-2024)
'Show history' action should be disabled in synchronize view for the deleted from repository resources (SBV-2025)
NullPointerException in decorators (SBV-2009)
Peg revision specified incorrectly for revision links (SBV-2026)
Incorrect highlight of current revision in case of repository resource history (SBV-2027)
Override and Update does not work for ignored resources (SBV-2028)
Refresh does not work on Repository View if same resource shown twice (SBV-2029)
Incorrect pop-up menu in case of file opened from repository. (SBV-2030)
Too big indention between controls on UI forms under Eclipse 3.0 (SBV-2031)
Current revision is not highlighted in histiory view after 'Update To' operation is performed (SBV-2035)
Relocate for the projects works incorrect if repository changes (SBV-2033)
Respect "conflicted" mark on working copy resource (SBV-1806)
JavaSVN fixes (in cooperation with TMate team):

java.lang.IllegalArgumentException: Negative time (SBV-1952)

special thanks to ngyen, yongyut
Get Resource List operation: ArrayIndexOutOfBoundsException (SBV-1934)

special thanks to Danny Mandel
Atomic commit fails for the projects checkouted from different repository locations (SBV-2007)

Version 1.0.0 RC3 [16 June 2006]

Features:

Improve usage of Subversive together with external SVN clients (SBV-2006)

special thanks to pkorros (forum user)
Copy resource URL to clipboard (SBV-1931)

special thanks to Chris Melikian
Add an ability to submit all forms by pressing Ctrl+Enter (as it is in commit dialog) (SBV-1980)

HistoryView - properties(). Support view of revision properties. (PLC-283)
In History View operations should be executed in background (SBV-1953)
Move property view to editor area (PLC-613)
Fixes:

Timing out when URL is encoded (contains %20 entries etc.) (SBV-1978)

special thanks to Turadg Aleahmad
Compare repository resources failure (SBV-1970)

special thanks to Danny Mandel
NPE in Show Messages operation (SBV-1938)

special thanks to Larry Edelstein
ClassCastException in Subversive code (SBV-1932)

special thanks to Larry Colson
NPE in Compare Resource with Revision operation (SBV-1936)

special thanks to Gregory Gerard
Trunk, branches and tags default values are not stored if they are disabled while creating new location

special thanks to contributor Sergey Vasilchenko for provided patch
Export does not work if destination folder entered manually (not selected from picker) (SBV-1993)

Validate all UI forms layout and optimize their content if it's necessary (SBV-1981)
AssertionFailedException while closing Repository Browser (SBV-1964)
NPE while disposing AnnotateView (SBV-1990)
"Hide unrelated" option works incorrectly in case of moved/copied resources (SBV-1998)
Create Tags/Branches/Trunk does not work in some cases (SBV-1992)
NullPointerException in merge dialog (SBV-1973)
Override And Commit: NullPointerException (SBV-1977)
Separate SSL callback from the general one (SBV-1958)
Repository locations is not refreshed some time (SBV-1946)
Subversive doesn't allow underscore in repository host name. Add ability to support. (SBV-1943)
Delete operation: Errors occurred while refreshing resources with the local file system (SBV-1940)
ArrayOutOfBoundsException in HistoryView (SBV-1929)
Version 1.0.0 RC2 [2 June 2006]

Features:

Add Break Lock operation to Repository View (SBV-1895)
Notification of Resource Selection Change in ICommentDialogPanel (SBV-1882)
Remember & prefill comment message when "Cancel" is pressed in previous commit try (SBV-1803)
Incoming deletion for project should disconnect project from source control without meta-inforamtion deletion (PLC-1184)
Fixes:

Some time default editor is not opened if the editor registered to specific file type is not opened (SBV-1925)

special thanks to Robert r. Sanders
ConcurrentModificationException while changing repository location properties (SBV-1884)

special thanks to Tjedrzejczak
Missing import "org.eclipse.help" in feature.xml (SBV-1914)

special thanks to Christian Buggle
Override And Update: Errors occurred while refreshing resources with the local file system (SBV-1903)

special thanks to Matias
Can't find file when synchronising (SBV-1910)

special thanks to Chris Melikian
Deadlock while opening project (SBV-1701)

special thanks to Jeremy Hare
Compare Resource with Revision fails for replaced files (SBV-1885)

special thanks to Joerg von Frantzius
BadLocationException in SVN Annotate View (SBV-1780)

special thanks to Alex Ostrovsky
[Subversive] Report ID-TDB4K - Prepared Tag Operation Failure Report (SBV-1827, SBV-1893)

special thanks to jmilora
Incorrect URL validation on repository properties editing form (SBV-1772)

special thanks to Hans van der Meer
Discard Repository Location operation does nothing if there is at least one location in the set that could not be discarded (SBV-1892)

Validate forms UI on Linux systems (SBV-1900)
Incoming project deletions does not handled by Override and Update action (SBV-1916)
NPE in time of merge operation (SBV-1902)
"Replace with" actions fails if non-versioned files exists in the directory to be replaced (SBV-1807)
Disable 'Compare with previous revision' item in the pop-up menu for some of affected paths (SBV-1881)
Mark As Merged Operation fails if project tree is not in sync with file system (SBV-1820)
"Compare with previous revision" fails for the affected paths in History View because of malformed url (SBV-1880)
".project" and ".classpath" file addition cannot be updated (SBV-1879)
Project created using Check out/New Project Wizard should respect project settings (SBV-1889)
JavaSVN features (in cooperation with TMate team):

SVNClientEx::mergeStatus() enhancement (SBV-1888)
JavaSVN fixes (in cooperation with TMate team):

Certificate bug in subversive (SBV-1810)

special thanks to Chris West
Allow caching of SSL certificates (SBV-1887)

SVNClient::info2() acquires authentication four times (SBV-1886)
SVNClientEx::merge() fails when it called second time (SBV-1825)
SVNClientEx::merge() trims resource name and fails (SBV-1894)
Version 1.0.0 RC1 [19 May 2006]

Features:

Project label decorator improvements (PLC-1089)

special thanks to Arvoreen (forum member)
Support of the tsvn:logtemplate property (PLC-1219)

special thanks to axiom10 (forum member)
Comment Templates like in CVS (PLC-1422)

special thanks to Clint Dovholuk
Support ASP.NET hack (PLC-1365)

special thanks to Clint Dovholuk
It is not possible to branch/tag multiple projects at once (PLC-783)

special thanks to Berserksangr (forum member)
Fixes:

Invalid location of .project and .classpath files after check out (SBV-1822)

special thanks to Angelo (forum user)
Incorrect error message in in time of Checkout if target folder is locked by external process (SBV-1756)

special thanks to Turadg Aleahmad
Allow Override and Update for new files (SBV-1589)

special thanks to Dotjerky (forum user)
NPE in Commit Operation (SBV-1615, SBV-1815)

special thanks to Paul Kendall, Christian
Errors occurred while refreshing resources with the local file system (SBV-1561, SBV-1588)

special thanks to Tjedrzejczak, Dumitru Frunza
Incorrect URL validation on repository properties editing form (SBV-1772)

special thanks to Hans van der Meer
Show Repositories View Operation Failure Report (SBV-1763)

special thanks to Simon Liu, Axel Bock
Problem with Compare (SBV-1710)

special thanks to David Harrigan
Wrong dialog text for browsing url for merging (SBV-1767)

special thanks to Danny Mandel
NoClassDefFoundError PluginIDVisitor

special thanks to Steve Zadoorian
Report shouldn't be sent for the network communication problems (SBV-1781)

Incoming deletion for project should delete project from workspace (PLC-1184)
URL Validation failed on GNU JVM (SBV-1657)
Check Out As action failed (SBV-1808)
Validate UI forms (SBV-1785)
No actions in the context menu for a resource in "strange" state (PLC-800)
NPE in CreatePatchAction (SBV-1757)
JavaSVN fixes (in cooperation with TMate team):

Exception in case if WC is svn:externals in parent WC (SBV-1692)

special thanks to Sascha Frick
Unknown node kind '3' in merge operation (SBV-1654, SBV-1653, PLC-1380, PLC-1187)

special thanks to Edward Seymour, Danny Mandel
Commit failed with "502 Bad Gateway" error (PLC-1439)

special thanks to Bpasero and Oliverh (forum members)
Unable to register repository with only server name in URL (SBV-1790)

special thanks to Hugi (forum member)
Version 1.0.0 M12 [5 May 2006]

Features:

Add "Stop On Copy" option to History View (PLC-704)
Hide unrelated paths option for History View (PLC-703)
Let user decide to override existing folders while checkout or not (SBV-1686)
Arrange checkout menu items (PLC-1204)
Add UI part of the proxy callback support (PLC-955)
Fixes:

Error encountered: null argument provided to table view (SBV-1582)

special thanks to Yogesh B Kanitkar
[Subversive] Share Project operation FAILURE REPORT (PLC-1402)

special thanks to Peter Rose
Report ID-CAYHC - Show Properties Operation Failure Report (SBV-1658)

special thanks to Ken Geis
Unaccessible API's on GNU JRE (SBV-1673)

special thanks to Martin Zuber
Report ID-HGXUD - Prevented recursive attempt to activate part (PLC-1368)

special thanks to Tom Staubitz
Compare with BASE requires connections to server (SBV-1567)

special thanks to Erik Dick
Strange merge behavior (PLC-1369)

special thanks to Danny (forum user)
Typo in a dialog (SBV-1695)

Invalid merge()/mergeStatus() behaviour (SBV-1526)
Report ID-MXE52 - ContentViewer must have a content provider HistoryView
Report ID-PD8W6 - ContentViewer must have a content provider AnnotateView
Report ID-B7MW0 - Add Repository Location Operation Failure Report (SBV-1685)
Address already in use: connect (SBV-1574)
Cannot compare resources (PLC-WLG10K)
Hierarchy of added resources not completely visible in the Structure Compare (PLC-791)
Many warning dialogs and log records while comparing two revisions (PLC-790)
"Compare with revision" operation fails for branched(tagged) resource (PLC-592)
Compare two revision is extremely slow (PLC-588)
'Compare with revision' operation fails after moving the resource (PLC-578)
Refactor fails when changing package name (SBV-1655)
JavaSVN fixes (in cooperation with TMate team):

Unrecognized node kind '0' in time of merge action (PLC-1500)

special thanks to Edward Seymour
Checkout failed because of Status-Line '0' (SBV-1592)

special thanks to fjalvingh (forum user)
Malformed network data; Cannot open session, you need to establish a connection first. (SBV-1599, SBV-1597, SBV-1558, SBV-1663)

special thanks to Chad Woolley, Jörg Henne
diffStatus fails when two files is compared (SBV-1553)

Version 1.0.0 M11 [21 April 2006]

Features:

Respect hierarchical structure in Checkout Projects (PLC-1397)

special thanks to Memelet (forum member)
Obtain project name from .project file (if so) during checkout from repository (PLC-1413)

Fixes:

Attempted to beginRule: R/, does not match outer scope rule: P/ (SBV-1550, SBV-1587, SBV-1622, SBV-1627)

special thanks to Mathis Hofer; MBertier; Konstantin Haas; Sebastian Hardt; Mitsu Hadeishi; Barry Kaplan
Add Repository Location Operation Failure (widget is disposed) (SBV-1532)

special thanks to John N Underwood
The commit dialog looks confusing (SBV-1606, FastTrack-PLC-1528)

special thanks to Christian Nelson
NullPointerException if DefaultDialog::open() fails (SBV-1628)

Check Out Operation Failure Report ID-E3SG4 (PLC-1420)
NullPointerException if SVNClient::info() operations fails due to some reason (SBV-1580)
Repository View "Move To..." action does not work (SBV-1557)
JavaSVN fixes (in cooperation with TMate team):

Broken workspace in case of case-sensitive rename (SBV-1528, SBV-1522)

special thanks to Kiel Hodges
Check Out Operation Failure Report (IndexOutOfBoundsException) (PLC-1470)

special thanks to Kevin Ross
NPE in SVNFileUtil (SBV-1602)

mergeStatus() operation ingnores IProgressMonitor.isActivityCancelled() (PLC-1463)
Resource names is encoded for mergeStatus() (PLC-1462)
Version 1.0.0 M10 [7 April 2006]

Features:

Support of shortcuts

special thanks to Georges-Etienne Legendre;Christian Nelson
Include changes to commit dialog like in CVS

special thanks to Daniel Spiewak, aochsner (forum user)
Implement 'Copy' and 'Move' operations for the repository exploring perspective

Implement extension point that alows configure email report properties
Support for synchronize action contributions
Create patch implementation
Fixes:

Could not instantiate provider org.tigris.subversion...

special thanks to Maxim Gordienko; Barry Kaplan; Johannes Matheis; Ralph Navarro;Turadg Aleahmad
Massive CPU usage - Eclipse slowdown

special thanks to Clint Dovholuk
Excessive "Build Workspace" and slowdown

special thanks to Clint.Dovholuk; Mike (forum user)
NullPointerException in time of Share Project operation

special thanks to Hans van der Meer
NullPointerException when operation is cancelled

special thanks to Tjedrzejczak
NullPointerException in LocalInfoPage

special thanks to Andreas Andreou
Incorrect icon for modified resources in preview

Cleanup menu is enabled for non-versioned resources
NPE in time of project set import
Default focus in the New Repository Location Wizard should be to the field Root URL
NullPointerException in FileUtility.getOperableParents
NullPointerException in FileUtility.getResourcesRecursive
NullPointerException in AbstractSVNSyncInfo
NPE in Commit dialog
Checkout projects action reports 75% progress although it finished already
Error report sending is suggested for when SVNException is thrown
Support Eclipse 3.2 linked resources
Resource out of sync with file system error
JavaSVN features (in cooperation with TMate team):

Enhance diff() functionality
JavaSVN fixes (in cooperation with TMate team):

Export operation fails with large files
Import operation fails on read-only path
Incoming addition cannot be merged
Resource names is encoded for mergeStatus()
Version 1.0.0 M9 [24 March 2006]

Features:

Add support for multiple folder creation in one transaction
Add file in SVN Repository view
Use CVS-like decoration icon for modified resources

special thanks to Eugene Kuleshov; Daniel Spiewak
Commit and Update buttons in Synchronize view toolbar

special thanks to Georges-Etienne Legendre
Set 'Don't send' button as a default for the error dialog

User input history should be implemented for name and email field in send error dialog
Fixes:

Resource '...' is not open" problem when project is closed under Eclipse 3.2Mx
Daniel Spiewak; Travis Hume

Switch error: outgoing changes in wc -> no switch possible

special thanks to ayampols our forum user
Incorrect page is shown in 'share project' wizard while sharing imported project (Eclipse 3.2Mx freezes)

special thanks to memelet (forum user); Georges-Etienne Legendre
Time-to-time error report window automatically closed with report sending

'There is an error occurs..' caption in repository browser
Cleanup operation also for folders

special thanks to Daniel Serodio our forum user
Invalid path separator used for UNIX-like systems

special thanks to anathaniel our forum user; D. Strauss; Leonard Soetedjo
ClassCastException in the SVNRemoteStorage class in time of RepositoryProvider check

Merge, switch dialogs select revision for the wrong resource (should agree with input url)
Error report preview fails under Eclipse 3.2Mx
NPE in History View in some hard cases
NPE during a refresh of a project

special thanks to Frits Jalvingh
Hiding History View parts works incorrect

Version 1.0.0 M8 [17 March 2006]

Features:

Improve merge dialog
Mark top revision in History View in Repository Mode

special thanks to Daniel Spiewak
Rework History View - comment viewer should be shown in the bottom of the log messages table

special thanks to Eugene Kuleshov
Optimize "Edit repository properties" panel

Add Subversive version id to the error report
Add sequence number for the mail error report
Fixes:

Sort by date in resource history view works incorrect
Concurrent modification exception

special thanks to Cedric Pineau
java.lang.NumberFormatException in repository browser

Composite operation should recognize not executed depended operation.
Checkout as using new project wizard works incorrect
Get Resource List operation FAILURE REPORT

special thanks to Jon our bug reporter.
Pre-close/Pre-delete Clear operation FAILURE REPORT

special thanks to Cedric Pineau
NPE during Share project operation

special thanks to Kevin O'Neill; Cedric Pineau; Barry Kaplan; David Saff
Make error report preview form platform independent

special thanks to Cedric Pineau
Null pointer exception then Synchronize View is closed

special thanks to Leonard Soetedjo
Changes of the New Project Wizard during checkout are lost

special thanks to Armen our forum member
Share project fails when project layout structure partially exists on the repository

Repository view navigator makes unneccessary requests to the server
Null pointer exception in select revision panel when no network available
NPE in LogMessagesComposite
Override and commit & markAsMerged operations work incorrect in case replaced resources
Checkout projects action can't be completed if common error occurs
Repository scanning can't be cancelled
Checkout overrides projects without warning
Simply notify user when an error occurs during send report . Do not ask it to send this error
Rework SVN views description according Eclipse IDE standart
Invalid working behaviour for replaced resources
Null pointer exception in History view then no network connection available
Repository browsing panel works incorrect in case no network connection available
All compare with ... operation asks to send report when no network available
Null pointer exception in affected paths composite
ClassCastException in Repository Browsing Panel
Subversive propose to send email report when repository folder already exists
NPE during send a report

special thanks to Danny Mandel
Affected paths view shows incorrect information

NPE in Repository Properties
special thanks to Danny Mandel
Version 1.0.0 M7 [10 March 2006]

Features:

Change Preferences->Team UI like in Eclipse/CVS 3.1 [usability]
Improve error reporting dialog [usability]
Fixes:

Team menu should be ordered like in CVS
special thanks to Daniel Spiewak for reporting this issue
Widget disposed error
special thanks to Daniel Spiewak for reporting this issue
Create new repository location operation from 'select wizard dialog' fails
Add ability to show properties on the repository roots (TRUNK, TAGS, BRANCES and ROOT)
Changing history view layout works incorrect
JavaSVN fixes:

Incorrect cancelation of SVN Checkout
Checkout freezes when cancel button is pressed
Version 1.0.0 M6 [7 March 2006]

Features:

Add option to mail report (Do not ask me to send report in future) [usability]
Fixes:

Show annotation operation failure
Simply notify user when an error occurs during send report. Do not ask it to send this error
Authentification problem for "send error report"
Null pointer exception in check out as operation
Add ability to subscribe on project state changed events
Synchronize is called for the project which is not shared yet
Version 1.0.0 M5 [4 March 2006]

Features:

Api for PropertyManager [extension points]
Add �Refresh� button to SVN Repository Browser toolbar [usability]
Support Eclipse 3.2 [functionality]
Add ability to open and compare with previous revision for the affected paths in History View [usability]
Provide ability to send e-mail reports for non-SVN errors [functionality]
Fixes:

Refresh on SVN Repository Browser work incorrectly
Action "Edit Properties" throws java.lang.IllegalArgumentException
NPE on the Repositories View when *.psf is imported
Override and Commit operation fails
Error window is shown twice for the same error
Empty select revision dialog is shown
Paging shows correct number of revisions only at first time
Compare reports "operation failed", but in the end the comparison is displayed
Quick filter doesn't work in the selection picker
Validate and amplify messages on the plugin UI forms
JavaSVN fixes (in cooperation with TMate team):

SVNClientEx::diffStatus() should provide all possible information
SVNClient::properties() operations do not report an errors
SVNClientEx::merge() function do not merge files without conflicts
Version 1.0.0 M4 [24 February 2006]

Features:

Allow all connection modes supported by JavaSVN + its UI [functionality]
How to get IStorage instance in order to convert IResource->IRemoteResource [extension points]
Add ability to subscribe on project state changed events [extension points]
Fixes:

Unable to get unresolved resources from UpdateOperation
Show resource history view fails
Checkout operation works incorrect with equal project names
Annotation view works incorrect in package explorer
Show annotation works incorrect from history view
Version 1.0.0 M3 [17 February 2006]

Features:

Mark As Merged operation should supports properties [functionality]
Interactive merge [functionality]
Support of following connection modes: HTTP, HTTPS, SVN, SVN+SSH (password) [functionality]
Fixes:

Share project wizard does not work
Version 1.0.0 M2 [10 February 2006]

Features:

Show resource locks on repository view [functionality]
Show resource locks in the package explorer [functionality]
Add ability to copy() versioned folders between projects [functionality]
Design the default repository perspective layout [usability]
Fixes:

Operation 'move' on directory works incorrect in case different repository locations
Illegal 'Directory is out of sync with file system' error
ResourceChangeListener handles initial workspace delta badly
Override and commit operation fails
Properties / SVN Info fails
Paging support for the revision history
JavaSVN fixes (in cooperation with TMate team):

NullPointerException in time of diffStatus() operation
SVNclientEx::list() methods does not works with the SVN1.1.x repositories
Version 1.0.0 M1 [3 February 2006]

Features:

Lock/UnLock folder emulation [functionality]
Pass selected resource to ITeamHistoryFactory in the log message panel [extension points]
Repository browser improvements [usability]
ISVNClientInterfaceEx extension (resource deletion improvements) [functionality]
Enhance SVNClientEx::move() operation behavior (Refactor improvements) [functionality]
Decorate deleted folders [usability]
Add multi-line viewer for Property view [usability]
Double Atomic Commit [extension points]
Add ability to replace commit dialog [extension points]
Fixes:

Select revision wizard allows multi-selection, but only one revision is processed
Commit operation fails after deleting file directly from file system
JUnit tests integration to build process
Properties information is missing in the SVN Repositories perspective
Null pointer exception when Synchronize View is closed
NPE in AbstractConflictDetectionOperation.getUnprocessed()
JavaSVN fixes (in cooperation with TMate team):

Enhanced SVNClientEx::move() operation works incorrect
NullPointerException at commit time
Invalid lock comment returned
Add to SVN operation failed with NullPointerException
Add to version control operation failed
Checkout Operation failed with NullPointerException
Version 0.9.7 [27 January 2006]

Features:

Show hierarchical resource history [usability]
Add Import/Export ability to Repository View [usability]
Fixes:

Background operations cancellation
Wrong behavior of the synchronize action when SVN is not accessible
Validate UI forms
Version 0.9.6 [20 January 2006]

Features:

Validate user input on the UI forms [usability]
Add repository to IRevisionProvider [extension points]
Add "Keep Locks" option to commit dialog [usability]
Paging support for the revision history [usability]
Fixes:

Validate Forms UI
Java Compare Structure should be improved
Ugly error message after cancelled update
Cryptic and not entirely visible message if commit fails
Commit compare editor shows that remote file does not exist for all changed files
Cancel on the Resource History quick filter invokes an operation
Background operations cancellation
Close project operation fails
Copied from URL doesn't render real URL
Non default date/time pattern used
Synchronization progress monitor shows more than 100% done
JavaSVN Fixes (in cooperation with TMate team):

NullPointerException in time of checkout() operation
NullPointerException in status() operation with "remote" option set to true
Version 0.9.5 [13 January 2006]

Features:

Progress of update is not available in the sync. tree continuously [functionality]
Replacing properties without warning in Property View [functionality]
Fixes:

Null pointer exception on 'splitRepositoryLocations' operation
JavaSVN Fixes (in cooperation with TMate team):

No statuses about incoming updates if repository root is checked out
JavaSVN doesn't report any error while SVN Server does
Files in the root of the repository are not commited
JavaSVN does not support non-english resource names
Spelling error
Most of the operations (commit, update, cleanup etc) finish with obscure error
Version 0.9.4 [4 January 2006]

Features:

Enhance History View functionality ("Update To Revision..." and "Copy From URL/Rev") [functionality]
New repository location browser [usability]
"Reset Changes" button for "edit repository location" dialog [usability]
Fixes:

Project switches to branch, despite creating branch finishes with error
Properties View should works in standard way (using IActionOperation framework)
Revision number '-1' in synchronize view
Commit operation fails
A package and its file are reflected as damaged after deletion
Synchronize view shows incorrect information after commit deletion
"No changes" result on the parent of ignored resource, while it has conflict with the repository file
Second commit for the same file fails
Fixed ArrayIndexOutOfBoundsException
No changes found after rename operation
Choosing 'Show Annotation' action for the second time on the same file shows empty Annotate View
Double-click on the file in repositories view and history view doesn't switch to this file editor
Adding resource to svn:ignore by wildcard extension works incorrect
No warning dialog is shown while checking out development root (TRUNK, BRANCHES, TAGS) if it already exists in workspace
File shown incorrect revision number
