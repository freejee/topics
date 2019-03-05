# Metrics Server Flags

## Usage
* [flags]

## Flags

### --alsologtostderr
log to standard error as well as files

### --authentication-kubeconfig string
kubeconfig file pointing at the 'core' kubernetes server with enough rights to create tokenaccessreviews.authentication.k8s.io.

### --authentication-skip-lookup
If false, the authentication-kubeconfig will be used to lookup missing authentication configuration from the cluster.

### --authentication-token-webhook-cache-ttl duration
The duration to cache responses from the webhook token authenticator, (default 10s)

### --authorization-kubeconfig string
kubeconfig file pointing at the 'core' kubernetes server with enough rights to create subjectaccessreviews.authorization.k8s.io.

### --authorization-webhook-cache-authorized-ttl duration
The duration to cache 'authorized' responses from the webhook authorizer, (default 10s)

### --authorization-webhook-cache-unauthorized-ttl duration
The duration to cache 'unauthorized' responses from the webhook authorizer, (default 10s)

### --bind-address ip
The IP address on which to listen for the --secure-port port.<br>
The associated interface(s) must be reachable by the rest of the cluster, and by CLI/web clients.<br>
If blank, all interfaces will be used (0.0.0.0 for all IPv4 interfaces and :: for all IPv6 interfaces), (default 0.0.0.0)

### --cert-dir string
The directory where the TLS certs are located.<br>
If --tls-cert-file and --tls-private-key-file are provided, this flag will be ignored, (default "apiserver.local.config/certificates")

### --client-ca-file string
If set, any request presenting a client certificate signed by one of the authorities in the client-ca-file is authenticated with an identity corresponding to the CommonName of the client certificate.

### --contention-profiling
Enable lock contention profiling, if profiling is enabled

### --enable-swagger-ui
Enables swagger ui on the apiserver at /swagger-ui

### --help, -h
help for this command

### --http2-max-streams-per-connection int
The limit that the server gives to clients for the maximum number of streams in an HTTP/2 connection.<br>
Zero means to use golang's default.

### --kubeconfig string
The path to the kubeconfig used to connect to the Kubernetes API server and the Kubelets (defaults to in-cluster config)

### --kubelet-insecure-tls
Do not verify CA of serving certificates presented by Kubelets.<br>
For testing purposes only.

### --kubelet-port int
The port to use to connect to Kubelets (defaults to 10250) (default 10250)

### --kubelet-preferred-address-types strings
The priority of node address types to use when determining which address to use to connect to a particular node (default [Hostname,InternalDNS,InternalIP,ExternalDNS,ExternalIP])

### --log-flush-frequency duration
Maximum number of seconds between log flushes (default 5s)

### --log_backtrace_at traceLocation
when logging hits line file:N, emit a stack trace (default :0)

### --log_dir string
If non-empty, write log files in this directory

### --logtostderr
log to standard error instead of files (default true)

### --metric-resolution duration
The resolution at which metrics-server will retain metrics, (default 1m0s)

### --profiling
Enable profiling via web interface host:port/debug/pprof/ (default true)

### --requestheader-allowed-names strings
List of client certificate common names to allow to provide usernames in headers specified by --requestheader-username-headers.<br>
If empty, any client certificate validated by the authorities in --requestheader-client-ca-file is allowed.

### --requestheader-client-ca-file string
Root certificate bundle to use to verify client certificates on incoming requests before trusting usernames in headers specified by --requestheader-username-headers.<br>
WARNING: generally do not depend on authorization being already done for incoming requests.

### --requestheader-extra-headers-prefix strings
List of request header prefixes to inspect.<br>
X-Remote-Extra- is suggested, (default [x-remote-extra-])

### --requestheader-group-headers strings
List of request headers to inspect for groups.<br>
X-Remote-Group is suggested, (default [x-remote-group])

### --requestheader-username-headers strings
List of request headers to inspect for usernames.<br>
X-Remote-User is common, (default [x-remote-user])

### --secure-port int
The port on which to serve HTTPS with authentication and authorization.<br>
If 0, don't serve HTTPS at all, (default 443)

### --stderrthreshold severity
logs at or above this threshold go to stderr (default 2)

### --tls-cert-file string
File containing the default x509 Certificate for HTTPS.<br>
(CA cert, if any, concatenated after server cert).<br>
If HTTPS serving is enabled, and --tls-cert-file and --tls-private-key-file are not provided, a self-signed certificate and key are generated for the public address and saved to the directory specified by --cert-dir.

### --tls-cipher-suites strings
Comma-separated list of cipher suites for the server.<br>
If omitted, the default Go cipher suites will be use.<br>
Possible values: 
* TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
* TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
* TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
* TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
* TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
* TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305
* TLS_ECDHE_ECDSA_WITH_RC4_128_SHA
* TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
* TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
* TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305
* TLS_ECDHE_RSA_WITH_RC4_128_SHA
* TLS_RSA_WITH_3DES_EDE_CBC_SHA
* TLS_RSA_WITH_AES_128_CBC_SHA
* TLS_RSA_WITH_AES_128_CBC_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA
* TLS_RSA_WITH_AES_256_GCM_SHA384
* TLS_RSA_WITH_RC4_128_SHA

### --tls-min-version string
Minimum TLS version supported.<br>
Possible values: 
* VersionTLS10
* VersionTLS11
* VersionTLS12

### --tls-private-key-file string
File containing the default x509 private key matching --tls-cert-file.

### --tls-sni-cert-key namedCertKey
A pair of x509 certificate and private key file paths, optionally suffixed with a list of domain patterns which are fully qualified domain names, possibly with prefixed wildcard segments.<br>
If no domain patterns are provided, the names of the certificate are extracted.<br>
Non-wildcard matches trump over wildcard matches, explicit domain patterns trump over extracted names.<br>
For multiple key/certificate pairs, use the --tls-sni-cert-key multiple times.<br>
Examples: "example.crt,example.key" or "foo.crt,foo.key:*.foo.com,foo.com", (default [])

### --v Level, -v
log level for V logs

### --vmodule moduleSpec
comma-separated list of pattern=N settings for file-filtered logging