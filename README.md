Short answer: yes—you can use your own truststore and tell the Java scanner that pysonar launches to use it. There’s no “pysonar setting” for this, but Java honors system properties you can pass via env vars.

How to do it

1) Create your own truststore (no admin needed)

Windows (cmd):

keytool -importcert -trustcacerts -alias sonarServer ^
  -file C:\path\to\server.crt ^
  -keystore C:\Users\%USERNAME%\custom-truststore.jks ^
  -storetype JKS -storepass changeit

Linux/macOS:

keytool -importcert -trustcacerts -alias sonarServer \
  -file /path/to/server.crt \
  -keystore $HOME/custom-truststore.jks \
  -storetype JKS -storepass changeit

> keytool accepts PEM .crt files; you’ll be prompted to trust it—type yes.



2) Point the Java scanner to it

Set SONAR_SCANNER_OPTS before you run pysonar (same shell / same IntelliJ run config):

Windows (cmd):

set SONAR_SCANNER_OPTS=-Djavax.net.ssl.trustStore=C:\Users\%USERNAME%\custom-truststore.jks -Djavax.net.ssl.trustStorePassword=changeit -Djavax.net.ssl.trustStoreType=JKS
pysonar ...

PowerShell:

$env:SONAR_SCANNER_OPTS = "-Djavax.net.ssl.trustStore=$env:USERPROFILE\custom-truststore.jks -Djavax.net.ssl.trustStorePassword=changeit -Djavax.net.ssl.trustStoreType=JKS"
pysonar ...

Linux/macOS:

export SONAR_SCANNER_OPTS="-Djavax.net.ssl.trustStore=$HOME/custom-truststore.jks -Djavax.net.ssl.trustStorePassword=changeit -Djavax.net.ssl.trustStoreType=JKS"
pysonar ...

Using IntelliJ?

Put the same line in Run/Debug Configuration → Environment variables so the spawned Java process inherits it.


---

Notes & gotchas

This doesn’t replace the system cacerts; it just instructs Java to use your custom one for this process.

If you need to include both the default CAs and your self-signed cert, either:

Copy the original cacerts (if readable) and import your cert into the copy, or

Start from an empty JKS (as above). For most internal SonarQube setups, trusting only your server’s CA is fine.


If your server requires mutual TLS, you’d also set -Djavax.net.ssl.keyStore=... and its password; otherwise not needed.


If you tell me your OS and how you launch pysonar (terminal vs IntelliJ), I’ll tailor the exact commands for your setup.

