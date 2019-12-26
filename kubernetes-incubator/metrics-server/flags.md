# Metrics Server标记

## 用法
* [flags]

## 标记

SecureServingOptionsWithLoopback
SecureServingOptions

SecureServingOptions
BindAddress net.IP
BindPort int // BindPort is ignored when Listener is set, will serve https even with 0.
BindNetwork string // BindNetwork is the type of network to bind to - defaults to "tcp", accepts "tcp", "tcp4", and "tcp6".
Listener net.Listener // Listener is the secure server network listener. either Listener or BindAddress/BindPort/BindNetwork is set, if Listener is set, use it and omit BindAddress/BindPort/BindNetwork.
ServerCert GeneratableKeyCert // ServerCert is the TLS cert info for serving secure traffic
SNICertKeys []utilflag.NamedCertKey // SNICertKeys are named CertKeys for serving secure traffic with SNI support.
CipherSuites []string // CipherSuites is the list of allowed cipher suites for the server. Values are from tls package constants (https://golang.org/pkg/crypto/tls/#pkg-constants).
MinTLSVersion string // MinTLSVersion is the minimum TLS version supported. Values are from tls package constants (https://golang.org/pkg/crypto/tls/#pkg-constants).
HTTP2MaxStreamsPerConnection int // HTTP2MaxStreamsPerConnection is the limit that the api server imposes on each client. A value of zero means to use the default provided by golang's HTTP/2 support.

CertKey
CertFile string // CertFile is a file containing a PEM-encoded certificate, and possibly the complete certificate chain
KeyFile string // KeyFile is a file containing a PEM-encoded private key for the certificate specified by CertFile

GeneratableKeyCert
CertKey CertKey
CertDirectory string // CertDirectory is a directory that will contain the certificates. If the cert and key aren't specifically set this will be used to derive a match with the "pair-name"
PairName string // PairName is the name which will be used with CertDirectory to make a cert and key names It becomes CertDirector/PairName.crt and CertDirector/PairName.key

### --bind-address ip - BindAddress
The IP address on which to listen for the --secure-port port.<br>
The associated interface(s) must be reachable by the rest of the cluster, and by CLI/web clients.<br>
If blank, all interfaces will be used (0.0.0.0 for all IPv4 interfaces and :: for all IPv6 interfaces), (default 0.0.0.0)

### --secure-port int - BindPort
The port on which to serve HTTPS with authentication and authorization.<br>
If 0, don't serve HTTPS at all, (default 443)

### --cert-dir string - ServerCert.CertDirectory
The directory where the TLS certs are located.<br>
If --tls-cert-file and --tls-private-key-file are provided, this flag will be ignored, (default "apiserver.local.config/certificates")

### --tls-cert-file string - ServerCert.CertKey.CertFile
File containing the default x509 Certificate for HTTPS.<br>
(CA cert, if any, concatenated after server cert).<br>
If HTTPS serving is enabled, and --tls-cert-file and --tls-private-key-file are not provided, a self-signed certificate and key are generated for the public address and saved to the directory specified by --cert-dir.

### --tls-private-key-file string - ServerCert.CertKey.KeyFile
File containing the default x509 private key matching --tls-cert-file.

### --tls-sni-cert-key namedCertKey - SNICertKeys
A pair of x509 certificate and private key file paths, optionally suffixed with a list of domain patterns which are fully qualified domain names, possibly with prefixed wildcard segments.<br>
If no domain patterns are provided, the names of the certificate are extracted.<br>
Non-wildcard matches trump over wildcard matches, explicit domain patterns trump over extracted names.<br>
For multiple key/certificate pairs, use the --tls-sni-cert-key multiple times.<br>
Examples: "example.crt,example.key" or "foo.crt,foo.key:*.foo.com,foo.com", (default [])

### --tls-cipher-suites strings - CipherSuites
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

### --tls-min-version string - MinTLSVersion
Minimum TLS version supported.<br>
Possible values: 
* VersionTLS10
* VersionTLS11
* VersionTLS12

### --http2-max-streams-per-connection int - HTTP2MaxStreamsPerConnection
The limit that the server gives to clients for the maximum number of streams in an HTTP/2 connection.<br>
Zero means to use golang's default.











// DelegatingAuthenticationOptions provides an easy way for composing API servers to delegate their authentication to the root kube API server.
The API federator will act as a front proxy and direction connections will be able to delegate to the core kube API server
DelegatingAuthenticationOptions
RemoteKubeConfigFile string // RemoteKubeConfigFile is the file to use to connect to a "normal" kube API server which hosts the TokenAccessReview.authentication.k8s.io endpoint for checking tokens.
CacheTTL time.Duration // CacheTTL is the length of time that a token authentication answer will be cached.
SkipInClusterLookup bool
ClientCert    ClientCertAuthenticationOptions
RequestHeader RequestHeaderAuthenticationOptions

### --authentication-kubeconfig string - RemoteKubeConfigFile
kubeconfig file pointing at the 'core' kubernetes server with enough rights to create tokenaccessreviews.authentication.k8s.io.

### --authentication-token-webhook-cache-ttl duration - CacheTTL
The duration to cache responses from the webhook token authenticator, (default 10s)

### --authentication-skip-lookup - SkipInClusterLookup
If false, the authentication-kubeconfig will be used to lookup missing authentication configuration from the cluster.








// DelegatingAuthorizationOptions provides an easy way for composing API servers to delegate their authorization to
// the root kube API server.
// WARNING: never assume that every authenticated incoming request already does authorization.
//          The aggregator in the kube API server does this today, but this behaviour is not
//          guaranteed in the future.
type DelegatingAuthorizationOptions struct {
	// RemoteKubeConfigFile is the file to use to connect to a "normal" kube API server which hosts the
	// SubjectAccessReview.authorization.k8s.io endpoint for checking tokens.
	RemoteKubeConfigFile string

	// AllowCacheTTL is the length of time that a successful authorization response will be cached
	AllowCacheTTL time.Duration

	// DenyCacheTTL is the length of time that an unsuccessful authorization response will be cached.
	// You generally want more responsive, "deny, try again" flows.
	DenyCacheTTL time.Duration
}



### --authorization-kubeconfig string - RemoteKubeConfigFile
kubeconfig file pointing at the 'core' kubernetes server with enough rights to create subjectaccessreviews.authorization.k8s.io.

### --authorization-webhook-cache-authorized-ttl duration - AllowCacheTTL
The duration to cache 'authorized' responses from the webhook authorizer, (default 10s)

### --authorization-webhook-cache-unauthorized-ttl duration - DenyCacheTTL
The duration to cache 'unauthorized' responses from the webhook authorizer, (default 10s)











type FeatureOptions struct {
	EnableProfiling           bool
	EnableContentionProfiling bool
	EnableSwaggerUI           bool
}

### --profiling - EnableProfiling
Enable profiling via web interface host:port/debug/pprof/ (default true)

### --contention-profiling - EnableContentionProfiling
Enable lock contention profiling, if profiling is enabled

### --enable-swagger-ui - EnableSwaggerUI
Enables swagger ui on the apiserver at /swagger-ui




type MetricsServerOptions struct {
	// genericoptions.ReccomendedOptions - EtcdOptions
	SecureServing  *genericoptions.SecureServingOptionsWithLoopback
	Authentication *genericoptions.DelegatingAuthenticationOptions
	Authorization  *genericoptions.DelegatingAuthorizationOptions
	Features       *genericoptions.FeatureOptions

	Kubeconfig string

	// Only to be used to for testing
	DisableAuthForTesting bool

	MetricResolution time.Duration

	KubeletPort                  int
	InsecureKubeletTLS           bool
	KubeletPreferredAddressTypes []string

	DeprecatedCompletelyInsecureKubelet bool
}


### --kubeconfig string - Kubeconfig
The path to the kubeconfig used to connect to the Kubernetes API server and the Kubelets (defaults to in-cluster config)

### --metric-resolution duration - MetricResolution
The resolution at which metrics-server will retain metrics, (default 1m0s)

### --kubelet-port int - KubeletPort
The port to use to connect to Kubelets (defaults to 10250) (default 10250)

### --kubelet-insecure-tls - InsecureKubeletTLS
Do not verify CA of serving certificates presented by Kubelets.<br>
For testing purposes only.

### --kubelet-preferred-address-types strings - KubeletPreferredAddressTypes
The priority of node address types to use when determining which address to use to connect to a particular node (default [Hostname,InternalDNS,InternalIP,ExternalDNS,ExternalIP])

### --deprecated-kubelet-completely-insecure - DeprecatedCompletelyInsecureKubelet
Do not use any encryption, authorization, or authentication when communicating with the Kubelet.
This is rarely the right option, since it leaves kubelet communication completely insecure.  If you encounter auth errors, make sure you've enabled token webhook auth on the Kubelet, and if you're in a test cluster with self-signed Kubelet certificates, consider using kubelet-insecure-tls instead.







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










### --client-ca-file string
If set, any request presenting a client certificate signed by one of the authorities in the client-ca-file is authenticated with an identity corresponding to the CommonName of the client certificate.

### --vmodule moduleSpec
comma-separated list of pattern=N settings for file-filtered logging



### --alsologtostderr
log to standard error as well as files

### --log-flush-frequency duration
Maximum number of seconds between log flushes (default 5s)

### --log_backtrace_at traceLocation
when logging hits line file:N, emit a stack trace (default :0)

### --log_dir string
If non-empty, write log files in this directory

### --logtostderr
log to standard error instead of files (default true)

### --stderrthreshold severity
logs at or above this threshold go to stderr (default 2)

### --v Level, -v
log level for V logs

### --help, -h
help for this command





文件 metrics-server/cmd/metrics-server/app/start.go
方法 func NewCommandStartMetricsServer(out, errOut io.Writer, stopCh <-chan struct{}) *cobra.Command { }
添加 flags.BoolVar(&o.DisableAuthForTesting, "disable-auth-for-testing", o.DisableAuthForTesting, "Disable auth for testing only.")

命令行参数
# --disable-auth-for-testing=true 自己添加的配置项
--disable-auth-for-testing=true
--kubeconfig=C:\Users\huangqs\.kube\config
# --kubelet-insecure-tls=true 暂时不能用这个，兼容性不够
--deprecated-kubelet-completely-insecure=true
--kubelet-preferred-address-types=InternalIP
--kubelet-port=10255






















